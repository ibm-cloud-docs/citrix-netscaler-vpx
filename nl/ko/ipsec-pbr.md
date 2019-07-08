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

# PBR(Policy Based Routing) 작성
{: #creating-policy-based-routing}

PBR(Policy Based Routing) 정책은 VPN 연결에서 사용할 고유 트래픽 매개변수(예: 로컬 및 원격 서브넷)를 지정하는 데 필요합니다. PBR 프로파일을 작성하려면 다음 단계를 수행하십시오.

1.	**시스템 > 네트워크 > PBR**로 이동하여 **추가**를 선택하십시오.
2.	**이름**을 입력하십시오.
3.	**조치**를 기본 설정인 **허용**으로 남겨두십시오. 
4.	**다음 홉 유형**에 대해 **IP 터널**을 선택한 후 **IP 터널 이름** 드롭 다운 목록에서 [이전된 작성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel)된 터널을 선정하십시오.
5.	**PBR 사용**을 선택했는지 확인하십시오.
6.	**IP 구성** 섹션에서 **오퍼레이션** 필드에 대해 **=**를 선택하십시오(소스 및 대상 모두에 해당). 
7.	다음 필드에서 첫 번째와 마지막 서브넷 IP를 지정하십시오. 
  *	**소스 IP 낮음**
  *	**소스 IP 높음**
  *	**대상 IP 낮음**
  *	**대상 IP 높음**
8.	**작성**을 클릭하십시오.

    <img src="images/ipseCreatePBR1.png" alt="그림" style="width: 200px;"/>

9.	**시스템 > 네트워크 > PBR**에서 새 PBR을 선택하고 **조치 선택** 목록을 클릭한 후 **적용**을 선택하십시오.

    <img src="images/ipsecCreatePBR2.png" alt="그림" style="width: 600px;"/>

CLI에서 PBR 프로파일을 작성하려면 다음 구문을 사용하십시오. 

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs
  
  ```
  {: codeblock}

  VPN 터널을 거쳐 VPX 후방에 있어야 하는 가상 서버 인스턴스 또는 인프라는 VPX를 기본 게이트웨이로 사용하거나 정적 라우트를 사용하도록 구성되어야 함을 유념하십시오. 대상이 원격(피어) 서브넷인 경우 이는 VPX로 트래픽을 전송합니다. 아래의 정적 라우트(**10.115.0.0/16**) 예를 참조하십시오.
  {: note}

  ```
  >route print
  ===========================================================================
  인터페이스 목록
  3...06 93 7a 03 f0 b3 ......XenServer PV 네트워크 디바이스 #0
  4...06 ff 8f 6d 89 e8 ......XenServer PV 네트워크 디바이스 #1
  1...........................소프트웨어 루프백 인터페이스 1
  7...00 00 00 00 00 00 00 e0 Microsoft ISATAP 어댑터 #2
  10...00 00 00 00 00 00 00 e0 Microsoft ISATAP 어댑터 #3
  ===========================================================================
  
  IPv4 라우트 테이블
  ===========================================================================
  활성 라우트:
  네트워크 대상            넷마스크          게이트웨이       인터페이스        메트릭
          0.0.0.0          0.0.0.0    169.54.255.65    169.54.255.73     26
       10.115.0.0      255.255.0.0      192.168.0.1      192.168.0.2     26

  ```
  {: codeblock}
