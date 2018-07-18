---
copyright:
  years: 1994, 2017
  
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX 소프트웨어 어플라이언스 시작하기

{{site.data.keyword.BluSoftlayer_notm}} 솔루션에 Citrix NetScaler VPX를 배치하면 웹 애플리케이션 제공이 가속화되고 성능이 향상되며 클라우드 애플리케이션 및 서비스가 최적화되고 사용 가능하며 안전한 상태로 유지됩니다. 게임, 빅데이터 및 분석과 같은 까다로운 워크로드나 프라이빗 클라우드가 있는 경우 Citrix NetScaler VPX는 가장 필요한 때에 가장 필요한 위치에 가장 필요한 방법으로 솔루션을 제공하는 데 도움이 될 수 있습니다.

## 시작하기 전에
Citrix NetScaler VPX를 시작하려면 다음 정보를 알고 있어야 합니다.

* IBM Cloud 고객 포털 로그인 정보
* 로드 밸런서의 배치 위치
* 사용자 요구에 가장 맞는 Netscaler 유형(자세한 정보는 [Load Balancers 탐색](https://console.bluemix.net/docs/infrastructure/loadbalancer-service/explore-load-balancers.html) 참조)
* 필요한 공인 IP 주소 수
* 로드 밸런서를 지정할 VLAN

## Citrix NetScaler VPX 주문

Citrix NetScaler VPX 소프트웨어 어플라이언스를 주문하려면 고객 포털의 주문 페이지로 이동하십시오.

1. 브라우저에서 [고객 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){: new_window}을 열고 계정에 로그인하십시오.
2. 고객 포털 탐색에서 **디바이스 > 디바이스 목록**을 선택하고 **디바이스 주문** 링크를 클릭하십시오. 
3. **SoftLayer 제품 및 서비스 주문** 페이지에서 네트워크 섹션까지 아래로 스크롤하여 Citrix NetScaler VPX 아래의 **주문** 링크를 클릭하십시오.
4. 드롭 다운 메뉴에서 Citrix NetScaler VPX 소프트웨어 어플라이언스를 배치하려는 위치를 선택하십시오.  
5. 해당 소프트웨어 에디션, 소프트웨어 버전 및 처리량 요구사항에 가장 적합한 NetScaler 유형을 선택하십시오. 
6. 필요한 공인 IP 주소의 수를 선택하십시오.  
	이는 NetScaler VPX에 가상 IP 주소(VIP)로 배치되는 정적 공인 IP 주소입니다.
7. **계속**을 클릭하십시오.
8. 요청한 IP 주소에 대한 ARIN(또는 배치 지역의 해당 조직)에 필요한 정보를 입력하십시오.
9. 연락처 정보를 입력하십시오. 
10. VLAN을 선택하십시오. 
	대기 시간을 최소화하고 네트워크 리소스 활용이 최적화되도록 하려면 트래픽이 분배될 서버와 동일한 VLAN에 Citrix NetScaler VPX를 지정하십시오. 
11. 주문을 검토하고 이용 약관에 동의한 후 **주문하기**를 클릭하십시오. Citrix NetScaler VPX 소프트웨어 어플라이언스가 선택한 설정을 사용하여 배치됩니다. 

## 다음 단계

Citrix Netscaler VPX [기능](about-citrix-netscaler-vpx.html)에 대해 자세히 알아보거나 특정 Netscaler [용어](terminology.html)를 검토하거나 Netscaler [구성](netscaler-basic-configuration.html)을 시작할 수 있습니다.
