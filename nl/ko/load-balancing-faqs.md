---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}

# Citrix NetScaler VPX에 대한 FAQ
{: #faqs-for-citrix-netscaler-vpx}

다음은 Citrix NetScaler VPX에서 작업할 때 자주 질문되는 내용입니다.

## Citrix NetScaler VPX는 무엇입니까?
{:faq}

Citrix NetScaler는 성능을 가속화하고 애플리케이션 가용성 및 보호를 보장하며 운영 비용을 크게 줄여서 애플리케이션을 5배 향상시키는 ADC(Application Delivery Controller)입니다. 애플리케이션 요구사항을 충족하는 최적의 Citrix NetScaler 에디션을 선택하여 성능 요구사항에 맞게 적절한 전용 시스템에 배치하십시오. Citrix NetScaler에 대해 자세히 알아보려면 Citrix 웹 사이트에서 [NetScaler 페이지 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){:new_window}를 참조하십시오.

## 로드 밸런싱이 필요한 이유는 무엇입니까?
{:faq}

로드 밸런싱 트래픽은 애플리케이션 요청 및 로드를 여러 서버에 분배하기 때문에 많은 고객 구현의 핵심 측면이 되었습니다. 또한 다음을 포함하여 전체 토폴로지에 여러 가지 이점을 제공합니다.

* 보안. 애플리케이션 서버의 논리적 격리가 작성되거나 IP 프로토콜 및 포트 번호를 기반으로 트래픽 요청이 거부됩니다.
* 고가용성. 컨텐츠가 풀 또는 서버 그룹에 복제되어 호스트에 대한 가용성을 보장합니다.
* 확장성. 수요가 증가함에 따라 서버를 더 추가하여 로드 밸런서가 추가 서버에 워크로드를 분배하도록 할 수 있습니다.
* 효율성. 로드 밸런싱이 구성되면 워크로드가 동적으로 분배됩니다. 예를 들어, CPU와 같은 리소스를 보다 효율적인 방식으로 사용할 수 있습니다.

## {{site.data.keyword.BluSoftlayer_notm}}에서 사용 가능한 로드 밸런싱 옵션의 수는 몇 개입니까?
{:faq}

IBM© Load Balancer 오퍼링에 대한 자세한 비교는 [로드 밸런서 탐색](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)을 참조하십시오.

## NetScaler가 IPv6를 지원합니까?
{:faq}

예. IPv6 및 IPv4가 모두 {{site.data.keyword.BluSoftlayer_notm}} 공용 네트워크에서 지원됩니다.

## NetScaler가 사설 네트워크의 트래픽을 로드 밸런싱합니까?
{:faq}

예, NetScaler는 사설 네트워크로 확장되는 유일한 {{site.data.keyword.BluSoftlayer_notm}} 로드 밸런싱 제품입니다.

## NetScaler 어플라이언스의 소스 IP 대신 클라이언트의 소스 IP 주소를 보고하도록 NetScaler를 구성할 수 있습니까?
{:faq}

예, NetScaler 고급 관리 인터페이스 내에서 **소스 IP 사용(USIP)** 매개변수를 **YES**로 설정하여 NetScaler의 소스 IP 대신 클라이언트의 소스 IP를 보고하도록 할 수 있습니다.

어플라이언스에서 USIP 주소 모드를 사용으로 설정하면 서버와 통신할 때 IP 헤더에서 사용 가능한 클라이언트 IP 주소를 사용하도록 어플라이언스에 유연성이 추가됩니다. 이 모드를 사용으로 설정하면 어플라이언스가 클라이언트 IP 주소와의 서버 연결을 열고 연결 재사용 시 클라이언트 IP 주소를 고려합니다. 따라서 이 모드는 클라이언트 IP 주소를 기반으로 클라이언트당 제한된 재사용을 용이하게 합니다.

## HA 구성의 노드 간에 HA 관련 정보를 교환하는 데 사용되는 다양한 포트는 무엇입니까?
{:faq}

동기화 및 명령 전파를 위한 포트 3010. 하트비트 패킷을 교환하기 위한 UDP 포트 3003.

## 글로벌 서버 로드 밸런싱(GSLB)이 포함된 NetScaler VPX의 버전은 무엇입니까?
{:faq}

Platinum.

## NetScaler가 HA 구성에 포함될 수 있습니까?
{:faq}

예, NetScaler VPX 어플라이언스는 고가용성(HA) 구성을 지원합니다.

파트너가 있는 HA 모드로 구성되지 않으면 NetScaler VPX 서버가 중복되지 않습니다. 백업 및 복구 전략의 일부로 NetScaler VPX를 사용할 때 HA 환경을 배치하도록 적극 권장합니다.

또한 다른 하드웨어 및 소프트웨어 컴포넌트에 대한 중복성을 제공하는 것도 중요합니다. 예를 들어, 전원 공급 장치 및 로컬 디스크 드라이브에 중복성이 없을 수 있습니다. 이러한 컴포넌트에 장애가 발생하면 데이터가 손실될 수 있습니다.

## {{site.data.keyword.BluSoftlayer_notm}} NetScaler 오퍼링에 SSL VPN 기능이 포함되어 있습니까?
{:faq}

예, 이 기능은 NetScaler Gateway™로 알려져 있으며 모든 에디션에 포함되어 있습니다.  이 기능에 대한 자세한 정보를 보려면 [Citrix 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.citrix.com/products/netscaler-adc/){: new_window}를 방문하십시오.
