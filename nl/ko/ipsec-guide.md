---

copyright:
  years: 2019
lastupdated: "2019-04-28"

keywords: ipsec, vpn, vpx, tunnel

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

# IBM Virtual Router Appliance로 {{site.data.keyword.vpx_full}}의 IPSec 사이트간 VPN 구성
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

이 안내서에서는 Citrix VPX에서 IPSec VPN 사이트간 연결을 구성하기 위한 단계별 지시사항을 제공합니다. IBM Virtual Router Appliance(VRA)는 VPN 피어로 사용됩니다. 

<img src="images/ipsec1.png" alt="그림" style="width: 600px;"/>

## 배치 정보
이 배치는 다음 컴포넌트 스펙으로 빌드되고 테스트되었습니다.

| NetScaler VPX 버전 및 빌드	| VRA 버전 및 설명| 
| ------------- | ------------- | 
| NS12.1: 빌드 48.13.nc | AT&T vRouter 5600 1801q |

IPSec VPN을 구성하려면 VPX 플랫폼 라이센스가 필요합니다.
{: note}

## 시작하기 전에

이 안내서에서는 두 디바이스 모두의 소유권을 가정합니다. 주문에 대한 지시사항을 보려면 다음 링크를 방문하십시오. 

-	[{{site.data.keyword.vpx_full}} 소프트웨어 어플라이언스 시작하기](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[IBM Virtual Router Appliance 시작하기](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## 수행할 사항

이 안내서에서는 Citrix VPX 디바이스에서 IPSec VPN을 구성하는 방법을 알아봅니다.

태스크  |설명
------------- | -------------
[VPX의 필수 기능 사용](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) |우선 IPSec VPN 작성을 위한 필수 기능을 사용으로 설정하십시오. 
[IPSec 프로파일 작성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile) |IPSec 프로파일에는 연결 설정을 위한 보안 매개변수가 포함되어 있습니다. 
[IP 터널 작성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) |이 절에서는 프로토콜 매개변수와 함께 로컬 및 원격 IP 주소를 지정하기 위한 IP 터널 오브젝트를 작성합니다. 
[PBR(Policy Based Routing) 작성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing) | PBR은 로컬 및 원격 서브넷 모두에 대한 고유 트래픽 매개변수 정의에 사용됩니다. 
[VRA 구성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra) | 동등한 VPN 구성 구문을 사용하여 가상 라우터 어플라이언스를 구성합니다. 
[VPN 상태 확인](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection) | VPN 작동 상태를 확인하고 단순 연결 테스트를 실행합니다. 

## 추가 리소스
다음의 추가 리소스는 Citrix VPX 및 가상 라우터 어플라이언스에 대해 자세히 알아보는 데 도움이 될 수 있습니다.

* [CloudBridge 커넥터 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Citrix ADC 어플라이언스 및 Cisco IOS 디바이스 간의 CloudBridge 커넥터 터널 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Citrix VPX/ADC 12.1 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [추가 VRA 문서](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
