---

copyright:
  years: 2019
lastupdated: "2019-04-10"

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

# IP 터널 작성
{: #creating-ip-tunnel}

사용자는 로컬 및 원격 IP 주소와 함께 VPN 연결용 프로토콜 매개변수를 지정하기 위해 IP 터널 오브젝트를 작성해야 합니다. 이를 위해 다음을 수행하십시오.

1.	**시스템 > CloudBridge 커넥터 > IP 터널**로 이동하십시오. 
2.	**IPv4 터널 탭**에서 **추가**를 선택하십시오.
3.	다음 매개변수를 입력하십시오.
  *	이름
  *	원격 IP(원격 VPN 피어의 IP)
  *	원격 마스크
4.	로컬 IP 드롭 다운 목록에서 **서브넷 IP**(SNIP)를 선택하십시오. 
5.	**로컬 IP** 드롭 다운에서 VPN 엔드포인트로 사용될 적합한 SNIP를 선택하십시오. 
6.	드롭 다운 목록에서 **IPSEC**를 프로토콜로 선택하십시오. 
7.	**IPSec 프로파일 이름** 드롭 다운에서 [이전에 작성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx)된 프로파일 이름을 선택하십시오. 
8.	**작성**을 클릭하십시오.

    <img src="images/ipsecCreateIPtunnel.png" alt="그림" style="width: 200px;"/>

CLI에서 IP 터널을 작성하려면 다음 구문을 사용하십시오. 
  
  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1
  
  ```
