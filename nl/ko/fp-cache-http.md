---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, configure, configuration, http, traffic

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

# HTTP(S) 트래픽을 위한 캐시 경로 재지정 구성
{: #configure-cache-redirection-for-http-traffic}

HTTP 또는 HTTPS 트래픽을 위해 캐시 경로 재지정을 구성하려면 다음 단계를 따르십시오.

1. **트래픽 관리 > 캐시 경로 재지정 > 가상 서버**로 이동하여 **추가**를 클릭하십시오.
2. 정방향 프록시 가상 서버의 이름을 지정하십시오. 각 드롭 다운 목록에서 **HTTP** 프로토콜 및 **앞으로** 캐시를 선택하십시오. 그런 다음 사설 서브넷에서 IP 주소를 이 가상 서버에 지정하십시오.

	<img src="images/fp12.png" alt="그림" style="width: 300px;"/>

	**확인**을 클릭하여 계속하십시오.

3. 요약 페이지를 검토하고 **확인**을 클릭하십시오.  
4. **트래픽 설정**을 클릭하여 추가 구성 설정을 보십시오.
5. 트래픽 설정에서 요구사항에 따라 다음 세 가지 경로 재지정 옵션 중 하나를 선택하십시오.
	* **캐시** - 모든 아웃바운드 요청을 로컬 캐시 서버 풀로 경로를 지정합니다.
	* **정책** - 요청이 캐시 서버 풀 또는 대상 서버(원본)로 전달되어야 하는 경우 결정할 캐시 경로 재지정 정책을 확인합니다.
	* **원본** - 모든 아웃바운드 요청을 각 대상 서버(원본)로 경로를 지정합니다.

6. 드롭 다운 목록 **DNS 가상 서버 이름**에서 이전에 구성된 DNS 가상 서버를 선택하고 **경로 재지정** 옵션을 **원본**으로 설정하십시오.

	<img src="images/fp13.png" alt="그림" style="width: 300px;"/>

	**참고:** 아웃바운드 트래픽을 로컬 캐시 서버 풀로 경로를 지정하는 경우 **대상 가상 서버** 설정이 사용됩니다. 모든 아웃바운드 트래픽을 원본 서버로 경로를 지정할 때 비어 있는 상태로 두십시오.

7. **완료** 다음에 표시되는 **확인**을 클릭하십시오.
