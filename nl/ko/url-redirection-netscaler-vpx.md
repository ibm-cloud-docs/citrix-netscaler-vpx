---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix Netscaler VPX에서 URL 경로 재지정

NetScaler에서 `http://`로부터 `https://`로의 경로 재지정을 수행하는 가장 일반적인 방법은 백업/경로 재지정 기능을 활용하는 것입니다. 이 기능은 원래 "서버 중지" 또는 "유지보수" 페이지로 경로 재지정하기 위한 것이었습니다.  

이를 수행하려면 바인딩된 실제 서비스 없이 포트 80에서 청취 중인 가상 서버와 특정 `https://` URL으로의 백업 경로 재지정을 작성해야 합니다. 실제 가상 서버가 항상 "작동 중지"(바인딩된 활성 서비스가 없음) 상태이므로 백업 경로 재지정은 항상 활성 상태입니다. 명시적 경로 재지정 URL(예: https://web.example.com) 을 지정해야 하고 결과적으로 http://mail.example.com 에 액세스하려고 시도하는 사용자가 https://web.example.com 으로 경로 재지정될 수 있다는 단점이 있습니다.

호스트 이름/URL을 유지하면서 `http://`에서 `https://`로의 경로 재지정을 수행하는 대체 방법에서는 NetScaler의 "응답자" 기능을 사용합니다. 이 기능은 원래 정보를 포함한 HTTP 경로 재지정 메시지를 작성합니다. 이 작업은 몇 가지 간단한 단계로 수행됩니다. 아래 예에서 "w.x.y.z"를 HTTPS VIP의 IP 주소로 바꿔야 합니다.

1. 항상 성공할 모니터 유형(NetScaler가 작동 중인 동안에는 localhost ping 실행이 항상 온라인 상태임)을 준비하십시오.
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```
	
2. 사용되지 않을 IP(온라인 상태가 되지 않는 `1.1.1.1`에 있는 서버의 IP 주소)를 사용하여 허위 서비스를 정의하십시오.
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. 허위 서비스를 이전에 작성된 모니터에 바인드하여 항상 작동 상태로 보고되도록 하십시오.
	```
	bind lb monitor localhost_ping Always_UP_service
	```
	
4. 항상 작동 상태로 유지되는 서비스에 바인드하여 NetScaler가 항상 vserver의 포트 80을 청취하도록 하십시오.
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```
	
5. `http://`를 `https://`로 대체하도록 응답자 조치 및 정책을 작성하십시오.
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. NetScaler의 응답자 기능을 사용으로 설정하십시오(이 기능은 기본적으로 사용 안함으로 설정되어 있으므로 이 단계가 중요합니다).
	```
  enable ns feature responder
  ```
7. 청취 중인 vserver를 응답자 정책에 바인드하십시오.
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. 다음과 같이 'wget' 또는 'url'과 같은 명령행 유틸리티를 사용하여 의도한 대로 작동 중인지 확인할 수 있습니다.

```
wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

curl -v http://w.x.y.z
```

아래 예제에 따라 IP 주소 `w.x.y.z`를 URL 호스트 이름(예: http://mail.example.com 또는 http://web.example.com) 으로 대체하고 처음에 지정한 것과 동일하지만 "https"로 시작하는 호스트 이름이 "Location" 출력에 반영되었는지 확인하십시오.

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
