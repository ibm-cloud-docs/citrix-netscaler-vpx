---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, redirect, ssl, traffic

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# SSL 트래픽을 위한 캐시 경로 재지정 구성(선택사항)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

HTTP 또는 HTTPS 프로토콜을 사용하여 가상 서버를 위해 캐시 경로 재지정을 정의하는 대신(위의 단계에 설명된 대로) SSL 트래픽을 처리하도록 캐시 경로 재지정을 정의하려고 할 수 있습니다.

이를 수행하려면 다음 단계를 따르십시오.

1. **트래픽 관리 > 캐시 경로 재지정 > 가상 서버**로 이동하여 **추가**를 클릭하십시오. 정방향 프록시 가상 서버의 이름을 지정하고 SSL 프로토콜 및 **앞으로**의 캐시 유형을 선택하십시오. 사설 서브넷에서 필요한 포트와 함께 이 가상 서버에 IP 주소를 지정하십시오.

	<img src="images/fp14.png" alt="그림" style="width: 300px;"/>

	**확인**을 클릭하십시오.

2. 요약 페이지를 검토하고 **확인**을 클릭하여 계속 수행하십시오.
3. 경로 재지정, DNS 가상 서버 및 대상 가상 서버 구성을 지정하십시오.
4. **고급 설정** 패널 아래의 **인증서**를 클릭하여 구성과 관련된 SSL 인증서를 보십시오.
5. 비어 있는 필드인 **서버 인증서 없음**을 클릭하십시오.
6. 서버 인증서 선택 드롭 다운 목록에서 SSL 서버를 선택하십시오.
7. 필요한 인증서 구성 정보를 입력하십시오.

	<img src="images/fp15.png" alt="그림" style="width: 400px;"/>

	**설치**를 클릭하십시오.

8. **바인드**를 선택하십시오.

	<img src="images/fp16.png" alt="그림" style="width: 300px;"/>
