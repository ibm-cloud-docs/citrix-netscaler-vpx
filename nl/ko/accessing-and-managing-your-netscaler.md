---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX 관리
{: #managing-your-citrix-netscaler-vpx}

Citrix NetScaler 디바이스는 여러 가지 방법으로 {{site.data.keyword.BluSoftlayer_notm}} 솔루션을 개선하고 정제하는 데 도움이 되는 일련의 기능을 갖춘 강력한 도구입니다. 고객 포털에서 디바이스의 정보를 찾고 디바이스에 연결하여 해당 기능을 구성할 수 있습니다.  

## 고객 포털에서 NetScaler 세부사항 찾기

Citrix NetScaler 디바이스는 {{site.data.keyword.BluSoftlayer_notm}} 플랫폼에 있는 다른 모든 서버와 같이 디바이스 목록에 나열됩니다.

디바이스 목록을 찾으려면 다음을 수행하십시오.

1. 브라우저에서 [고객 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){: new_window}을 열고 계정에 로그인하십시오.
2. 고객 포털 탐색에서 **디바이스 > 디바이스 목록**을 선택하십시오.

디바이스가 디바이스 이름별로 정렬되어 표시됩니다. Citrix NetScaler VPX 디바이스의 디바이스 유형은 "NetScaler"입니다. 

NetScaler에 대한 행의 왼쪽에 있는 화살표를 클릭하여 행을 펼치고 NetScaler 관리 액세스를 위한 사용자 이름 및 마스킹된 비밀번호를 표시하십시오. 

디바이스 목록에 나열되는 기타 세부사항에는 다음이 포함됩니다. 

* 위치(NetScaler가 상주하는 데이터 센터)
* 사설 IP 주소(관리 기능을 위해 NetScaler에 연결하는 데 사용됨)
* 시작 날짜(시스템이 주문 및 프로비저닝된 시간)

**참고:** NetScaler의 사설 IP 주소는 포털에 나열되지만 NetScaler의 공인 IP 주소는 포털에 나열되지 않습니다. NetScaler 관리는 사설 IP 주소를 사용하여 수행되고 NetScaler 디바이스의 공인 IP 주소는 로드 밸런싱 서비스에 사용되는 디바이스의 VIP 또는 가상 IP로 사용되기 때문입니다.

## 디바이스 세부사항 화면 

NetScaler의 이름을 클릭하면 NetScaler에 대한 **디바이스 세부사항** 페이지로 이동합니다. 이 페이지에는 NetScaler가 배치된 VLAN과 NetScaler의 공인 IP 주소가 표시됩니다. 이러한 IP 주소는 NetScaler의 기본 공인 VIP 주소이므로 관리용으로 사용될 수 없습니다. 나중에 이러한 IP 주소를 사용하여 로드 밸런싱 서비스에 연관시킬 수 있습니다.

## NetScaler에 연결

{{site.data.keyword.BluSoftlayer_notm}}에서는 NetScaler 디바이스에 대한 전체 루트 액세스 권한을 부여합니다. NetScaler의 관리 UI에 로그인하려면 {{site.data.keyword.BluSoftlayer_notm}} 사설 네트워크({{site.data.keyword.BluSoftlayer_notm}} 관리 VPN 또는 {{site.data.keyword.BluSoftlayer_notm}} 환경 내의 서버에 대한 원격 세션에서 관리 기능 수행)에 연결되어야 합니다. 

고객 포털에서 NetScaler의 관리 UI에 연결하려면 **디바이스 세부사항** 화면의 오른쪽 상단 모서리에 있는 **조치** 드롭 다운 목록을 클릭하고 **디바이스 관리**를 선택하여 브라우저에서 새 탭 또는 팝업 창을 시작하십시오. 그러면 NetScaler의 NSIP(이전에 확인한 사설 IP 주소)로 라우팅됩니다. 표시되는 페이지에서 디바이스에 대한 루트 사용자 이름 및 비밀번호를 묻습니다. 정보를 입력하면 NetScaler 관리 GUI로 이동합니다. 

또는 NetScaler 디바이스의 사설 IP를 복사하여 웹 브라우저에 붙여넣을 수 있습니다.

### NetScaler SSH 액세스

선호하는 SSH 클라이언트를 사용하여 NetScaler 디바이스에 직접 연결할 수도 있습니다. 디바이스 목록 페이지에서 NetScaler 디바이스에 대한 사설 IP 및 로그인 정보를 사용하고 {{site.data.keyword.BluSoftlayer_notm}} VPN에 연결되었는지 확인하십시오. 
