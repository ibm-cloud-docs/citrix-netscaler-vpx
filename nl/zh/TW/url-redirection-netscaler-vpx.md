---
copyright:
  years: 1994, 2017

lastupdated: "2018-08-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix Netscaler VPX 中的重新導向 URL
{: #redirecting-urls-in-a-citrix-netscaler-vpx}

在 NetScaler 中執行 `http://` 到 `https://` 重新導向的最常見方法是運用備份/重新導向特性，而此特性一開始是要重新導向至「伺服器關閉」或「維護」頁面。  

若要這麼做，您必須建立虛擬伺服器，此虛擬伺服器會接聽埠 80、未連結實際服務，而且備份重新導向至特定 `https://` URL。實際虛擬伺服器一律會「關閉」（未連結即時服務），因此備份重新導向一律為作用中。缺點是您必須指定明確重新導向 URL（例如 `https://web.example.com`），因此，嘗試存取 `http://mail.example.com` 的使用者會被重新導向至 `https://web.example.com`。

執行 `http://` 到 `https://` 重新導向的替代方法會使用 NetScaler 的「回應者」特性，同時保留主機名稱/URL，而此特性會精心製作 HTTP 重新導向訊息（包括原始資訊）。這透過幾個簡單的步驟完成；在下面的範例中，請務必將 "w.x.y.z" 取代為 HTTPS VIP 的 IP 位址：

1. 準備一律會成功的監視器類型（只要 NetScaler 一啟動，即會對 localhost 進行 Ping 連線作業）。
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```
	
2. 利用永遠不會使用的 IP 來定義偽造服務（網址為 `1.1.1.1` 的伺服器 IP 位址絕對不會進行連線作業）。
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. 將偽造服務連結至先前建立的監視器，確保它一律報告為啟動。
	```
	bind lb monitor localhost_ping Always_UP_service
	```
	
4. 在 vserver 上，讓 NetScaler 一律接聽埠 80，並將它連結至一律保持啟動的服務。
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```
	
5. 撰寫回應者動作及原則，以將 `http://` 取代為 `https://`。
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. 啟用 NetScaler 的回應者特性（此步驟很重要，依預設會停用此特性）。
	```
        enable ns feature responder
	```
7. 將接聽 vserver 連結至回應者原則。
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. 您可以使用指令行公用程式（例如 'wget' 或 'curl'）確認這如預期運作，如下所示：
        
	```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

    curl -v http://w.x.y.z
    ```

將 IP 位址 `w.x.y.z` 替換為 URL 主機名稱（例如 `http://mail.example.com` 或 `http://web.example.com`），並確認 "Location" 輸出反映一開始指定的相同主機名稱，但開頭為 "https"，如下列範例所示：

```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z
    --2012-06-18 08:42:20--  http://w.x.y.z/
    Connecting to w.x.y.z:80... connected.
    HTTP request sent, awaiting response...
      HTTP/1.1 302 Moved Temporarily
      Location: https://w.x.y.z/
      Connection: close
      Cache-Control: no-cache
      Pragma: no-cache

    wget  -S --max-redirect 0 -O /dev/null http://web.example.com
    --2012-06-18 08:42:20--  http://web.example.com/
    Connecting to w.x.y.z:80... connected.
    HTTP request sent, awaiting response...
      HTTP/1.1 302 Moved Temporarily
      Location: https://web.example.com/
      Connection: close
      Cache-Control: no-cache
      Pragma: no-cache

    wget  -S --max-redirect 0 -O /dev/null http://mail.example.com
    --2012-06-18 08:42:20--  http://mail.example.com/
    Connecting to w.x.y.z:80... connected.
    HTTP request sent, awaiting response...
      HTTP/1.1 302 Moved Temporarily
     Location: https://mail.example.com/
      Connection: close
      Cache-Control: no-cache
      Pragma: no-cache
```
