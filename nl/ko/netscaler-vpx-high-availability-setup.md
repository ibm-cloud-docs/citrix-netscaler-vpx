---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: ha, high availability, setup, configure, configuration

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 고가용성(HA)을 위해 Citrix Netscaler VPX 설정
{: #setting-up-citrix-netscaler-vpx-for-high-availability-ha-}

로드 밸런서는 확장 가능한 애플리케이션의 성능과 안정성을 향상시키기 위해 여러 애플리케이션 서버에서 트래픽을 밸런싱하는 데 사용됩니다. 그러나 단일 로드 밸런서는 단일 장애 지점입니다. 고가용성(HA) Netscaler VPX 쌍을 구성하여 이를 방지하십시오. HA 쌍을 구성하려면 두 개의 Netscaler VPX 서버가 필요합니다. 기본 서버가 실패하는 경우 로드 밸런싱을 계속하기 위해 보조 서버가 사용됩니다.

서브넷 IP(SNIP)는 로드 밸런싱된 서버에서 Netscaler VPX의 가상 IP(VIP)에 작성된 요청(연결)의 소스 IP로 표시되는 IP입니다. 일반적으로 HA 쌍 설정에서는 SNIP가 변경되지 않지만 장애 복구 이벤트 중에 SNIP가 변경될 수 있습니다. 두 개의 Netscaler가 동일한 서브넷에 있는 경우 보조 Netscaler VPX의 SNIP가 원래 기본 Netscaler VPX에서 사용된 SNIP로 변경될 수 있습니다. 이로 인해 요청을 처리 중인 서버에 혼란이 발생하지 않습니다.

HA 구성의 경우 두 NetScaler가 모두 동일한 서브넷의 동일한 VLAN에 있어야 합니다.

HA 구성을 시작하기 전에 다음 전제 조건 조치를 수행해야 합니다.

1. 쌍이 활성-활성으로 구성될 경우 인스턴스에 추가되는 모든 VIP 서브넷이 "Routed to VLAN" 유형이어야 합니다.
2. 쌍이 활성-비활성으로 구성될 경우 인스턴스에 추가되는 모든 VIP 서브넷이 "Routed to VLAN" 또는 "Secondary routed to IP" 유형이고 기본 노드의 공인 IP 주소로 라우팅되어야 합니다.

필요한 VLAN에서 두 개의 Netscaler VPX 서버를 주문하고 HA 쌍 구성의 전제 조건을 충족하기 위해 VIP 및 SNIP 서브넷을 주문한 후 다음을 진행할 수 있습니다.

1. 두 개의 브라우저 창을 열고 두 NetScaler 모두의 고급 인터페이스에 로그인하십시오. 보조 NetScaler에서 **시스템 > 사용자 관리 > 사용자**로 이동하여 루트 비밀번호를 기본 NetScaler와 동일하게 설정하십시오. 그런 다음 디바이스 세부사항 페이지에서 {{site.data.keyword.BluSoftlayer_notm}} 포털의 파일에 대한 비밀번호를 보조에 대해 설정된 비밀번호와 일치하도록 업데이트하십시오.

2. 보조로 사용할 VPX에서 **시스템 > 고가용성**을 클릭한 후 첫 번째 행을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭하십시오. 고가용성 상태 구성 드롭 다운 상자에서 **보조 유지**를 선택하고 **확인**을 클릭하십시오.

3. **추가**를 선택하십시오. 다른 VPX의 시스템 IP 주소(기본의 High Availability 탭에 있음)를 입력하고 맨 아래에 루트 로그인 세부사항을 입력하십시오. **INC 켜기** 상자를 선택되지 않은 상태로 두십시오. **확인**을 클릭하십시오.

	IP가 동일한 서브넷에 없다는 오류가 수신되는 경우 두 VPX 서버가 동일한 VLAN에 없을 수 있습니다. 그렇지 않으면, 이제 기본 서버를 열고 **새로 고치기** 단추를 선택하여 두 서버가 모두 고가용성으로 작동 중임을 확인할 수 있어야 합니다.

	보조용 새 NetScaler 관리 IP는 이전보다 낮은 하나의 IP 주소입니다. 보조 VPX에 액세스할 수 없는 경우 명령행에서 다음을 사용하여 고가용성을 제거하십시오.

	`sh ha node`

	그런 다음 ha 노드가 될 항목을 제거하십시오.

	`rm ha node 1`

4. 기본 VPX에서 이제 원격 VPX가 동기화 중임을 확인할 수 있어야 합니다. 보조 서버로 이동하여 **네트워크 > IP** 구성을 확인하십시오. 기본 서버의 VIP와 기타 IP가 비활성(passive) 상태로 나열되어야 합니다.

6. 보조 서버에서 **시스템 > 고가용성**으로 돌아가서 **편집**를 클릭하십시오. 드롭 다운 상자에서 **사용**을 선택하고 **확인**을 누르십시오.

7. 강제로 장애 복구를 테스트하십시오. 화면을 새로 고치고 보조 서버에서 IP 주소가 활성(active) 상태가 되는지 지켜보십시오. 다시 장애 복구를 수행하고 비활성(passive) 상태로 전환되는지 지켜보십시오. IP에 대해 ping을 실행하여 작동하는지 확인하십시오.

8. 이제 기본 서버에 primary라는 레이블이 지정되어야 하고 보조 서버가 동기화 상태를 성공으로 보고해야 합니다.
