---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-6"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 기본 배치

[고객 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/)의 **디바이스 > 디바이스 목록**에서 NetScaler를 보면 NetScaler가 다른 서버와 다르게 표시되는 것을 알 수 있습니다. 즉, 디바이스에 사설 IP 주소가 있지만 공인 IP 주소는 없습니다.

{{site.data.keyword.BluSoftlayer_notm}}에서 NetScaler의 기본 배치는 사설 IP 주소를 관리 목적으로 사용되는 NSIP(NetScaler IP)로 자동 지정하여 가능한 안전하도록 디자인되었습니다. NetScaler의 왼쪽에 있는 화살표를 클릭하면 행이 펼쳐지고 기본 사용자 이름(root) 및 마스킹된 root 사용자 비밀번호가 표시됩니다. 

{{site.data.keyword.BluSoftlayer_notm}}는 프로비저닝 중에 많은 의사결정을 처리합니다. 예를 들어, 어떤 목적으로 어떤 IP 주소를 사용할지를 결정합니다. 어떤 VLAN을 배치에 사용할 것인지 묻습니다. 또한 스크립트 및 API를 사용하여 별도의 퍼블릭 및 프라이빗 VLAN에 인터페이스 지정 및 NSIP, VIP 및 SNIP를 포함한 각 인터페이스에 적절한 IP 주소 지정과 같은 많은 백엔드 구성을 자동화합니다.

## 무엇을 구성해야 합니까?

기본적으로 NSIP는 프로비저닝 중에 지정된 사설 IP 주소이며, 관리 목적으로 NetScaler에 연결하는 데 사용하는 IP 주소입니다. SNIP(서브넷 IP 주소)는 기본적으로 주문 프로세스 중에 선택한 VLAN에 있는 것과 동일한 기본 IP 서브넷에서 지정됩니다. 

의도한 로드 밸런싱된 서버가 상주하는 것과 동일한 VLAN을 선택한 경우 이러한 SNIP의 추가 구성이 필요하지 않습니다. 기본적으로 DNS는 {{site.data.keyword.BluSoftlayer_notm}}의 이름 서버로 설정됩니다. 기본 구현에서 {{site.data.keyword.BluSoftlayer_notm}}가 서버에 대한 DNS 레코드를 호스팅하는 경우 추가 구성이 필요하지 않습니다.
