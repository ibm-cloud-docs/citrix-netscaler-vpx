---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: proxy, traffic, appliance

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

# {{site.data.keyword.vpx_full}} 어플라이언스를 사용하여 정방향 프록시 트래픽 경로 재지정 구성
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

이 안내서는 {{site.data.keyword.vpx_full}} 어플라이언스를 사용하여 정방향 프록시 설정에 대한 단계별 구성을 제공합니다. 이 구성은 소프트웨어 버전 1.1(Platinum 기능 에디션) 및 10Mbps 성능을 실행하는 {{site.data.keyword.vpx_full}} 어플라이언스에서 테스트되었습니다.

<img src="images/fp1.png" alt="그림" style="width: 600px;"/>

## 수행할 사항
{: #what-you-ll-accomplish}

이 단계별 안내서에서는 서비스 구성 방법에 대한 정보를 제공합니다.

태스크  |설명
------------- | -------------
[{{site.data.keyword.vpx_full}} 주문](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) | {{site.data.keyword.vpx_full}} 어플라이언스를 주문하여 시작합니다.
[사설 서브넷 요청](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) | 사용자의 계정에 맞는 사설 서브넷을 IBM© 지원 센터에서 요청합니다.
[캐시 경로 재지정 및 로드 밸런싱 기능 사용](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) | 애플리케이션의 리소스를 식별합니다(예: 원본 풀 및 상태 검사 메커니즘).
[DNS 가상 서버 구성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) | DNS 분석기를 추가하고 DNS 서비스 그룹을 정의한 후 DNS 가상 서버를 정의합니다.
[HTTP(S) 트래픽을 위한 캐시 경로 재지정 구성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic) | HTTP 또는 HTTPS 트래픽을 사용하여 정방향 프록시 가상 서버를 위해 캐시 경로 재지정을 구성합니다.
[SSL 트래픽을 위한 캐시 경로 재지정 구성(선택사항)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) | HTTP 또는 HTTPS 대신 SSL 트래픽을 사용하여 정방향 프록시 가상 서버를 위해 캐시 경로 재지정을 구성합니다.
[아웃바운드 트래픽을 위한 소스 NAT 구성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) | {{site.data.keyword.vpx_full}} 어플라이언스를 활용하여 클라이언트 머신의 아웃바운드 트래픽에서 NAT를 수행합니다.
[클라이언트 머신의 인터넷 브라우저에서 프록시 설정 업데이트(선택사항)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) | 원하는 경우 클라이언트 머신의 인터넷 브라우저를 사용하여 프록시 설정을 업데이트합니다.
