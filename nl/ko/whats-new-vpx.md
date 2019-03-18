---
copyright:
  years: 1994, 2018
  
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX용 최신 업데이트
{: #recent-updates-for-citrix-netscaler-vpx}

## 버전 12.1

### 여러 개의 IP 주소가 있는 가상 서버
여러 개의 비연속적/연속적 IPv4 및 IPv6 주소가 있는 하나의 로드 밸런싱 가상 서버를 작성할 수 있습니다. 가상 서버에 바인드된 각 VIP 주소는 개별 가상 서버로 처리됩니다.

이 기능에 대한 자세한 정보는 Citrix 기사 [Multiple IP virtual servers ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}를 참조하십시오.

### SSL
다음 업데이트 항목이 SSL 연결에 적용되었습니다.
 
* DEFAULT_BACKEND 암호 그룹에서 취약한 암호 제거 
* Thales nShield® 외부 HSM의 프론트 엔드에 있는 ECDHE 암호에 대한 지원
* SafeNet 네트워크 외부 HSM의 프론트 엔드에 있는 ECDHE 암호에 대한 지원
* SSLv2 제거: NetScaler VPX 어플라이언스 릴리스 12.1에서는 SSLv2를 지원하지 않습니다.

12.1 SSL 업데이트에 대한 자세한 정보는 [Citrix 12.1 릴리스 정보 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}를 참조하십시오.

### GSLB를 위한 서비스 그룹 지원
이제 GSLB를 위한 IP 주소 기반 서비스 그룹, 도메인 이름 기반 서비스 그룹 또는 도메인 이름 기반 Auto-Scale 서비스 그룹을 구성할 수 있습니다. 또한 단일 서비스만큼 쉽게 서비스 그룹을 관리하고, 서비스 그룹을 가상 서버에 바인드하고, 서비스를 그룹에 추가할 수도 있습니다.

GSLB 서비스 그룹에 대한 자세한 정보는 Citrix 기사 [Configuring a GSLB service group ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}을 참조하십시오.
