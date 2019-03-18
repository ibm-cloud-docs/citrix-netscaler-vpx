---
copyright:
  years: 1994, 2017

lastupdated: "2018-08-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix Netscaler VPX での URL のリダイレクト
{: #redirecting-urls-in-a-citrix-netscaler-vpx}

NetScaler で `http://` から `https://` へのリダイレクトを実行する最も一般的な方法は、元々「サーバー・ダウン」ページまたは「保守」ページにリダイレクトするためのものであったバックアップ/リダイレクト機能を利用することです。  

これを行うには、実際のサービスがバインドされていないポート 80 で listen する仮想サーバーを作成し、特定の `https://` URL へのバックアップ・リダイレクトを作成する必要があります。 実際の仮想サーバーは常に「ダウン」(稼働中のサービスがバインドされていない状態) であるため、バックアップ・リダイレクトは常にアクティブです。 欠点は、明示的なリダイレクト URL (例えば、`https://web.example.com`) を指定する必要があるということと、結果として、`http://mail.example.com` にアクセスしようとしているユーザーが `https://web.example.com` にリダイレクトされることです。

ホスト名/URL を保持しながら `http://` から `https://` へのリダイレクトを実行する別の方法では、NetScaler の「レスポンダー」機能を使用して、元の情報を含む HTTP リダイレクト・メッセージを作成します。 これは、いくつかの簡単なステップで行います。以下の例では、「w.x.y.z」を HTTPS VIP の IP アドレスに必ず置き換えてください。

1. 常に成功する (NetScaler が稼働している限り、localhost の ping は常にオンラインになる) モニター・タイプを準備します。
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```
	
2. 決して使用されない IP (決してオンラインにならない、`1.1.1.1` のサーバーの IP アドレス) を使用して偽のサービスを定義します。
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. 偽のサービスを、以前に作成したモニターにバインドして、常に、稼働中と報告されるようにします。
	```
	bind lb monitor localhost_ping Always_UP_service
	```
	
4. NetScaler が常に vserver 上のポート80 を listen するようにし、常に稼働しているサービスにバインドします。
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```
	
5. レスポンダーのアクションとポリシーを作成して、`http://` を `https://` に置き換えます。
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. NetScaler のレスポンダー・フィーチャーを有効にします (このフィーチャーはデフォルトでは無効になっているため、このステップは不可欠です)。
	```
        enable ns feature responder
	```
7. listen している vserver をレスポンダー・ポリシーにバインドします。
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. 「wget」や「curl」などのコマンド・ライン・ユーティリティーを以下のように使用して、これが、意図したとおりに機能していることを確認できます。
        
	```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

    curl -v http://w.x.y.z
    ```

IP アドレス「`w.x.y.z`」を URL ホスト名に置き換え (例えば、`http://mail.example.com` または `http://web.example.com`)、「Location」出力が、最初に指定されたものと同じホスト名を反映しているが、以下の例のように「https」で開始されていることを確認します。

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
