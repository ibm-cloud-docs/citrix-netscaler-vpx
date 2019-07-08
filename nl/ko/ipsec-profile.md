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

# IPSec 프로파일 VPX 작성
{: #creating-ipsec-profile}

IPSec 프로파일에는 연결 설정을 위한 보안 매개변수가 포함되어 있습니다. 프로파일을 작성하려면 다음 프로시저를 수행하십시오.

1.	**시스템 > CloudBridge 커넥터 > IPSec 프로파일**로 이동하여 **추가**를 클릭하십시오.
2.	다음 매개변수를 입력하십시오.
  *	**이름**
  *	**암호화 알고리즘**
  *	**해시 알고리즘**
  *	**수명**
3.	적합한 **IKE 프로토콜 버전**을 선택하십시오.
4.	원하는 경우에는 **완전 순방향 비밀성(PFS)**을 선택하십시오.
5.	**사전 공유된 키(PSK) 존재**를 선택하고 **값** 필드에 PSK를 입력하십시오. 
6.	**작성**을 클릭하십시오.

    <img src="images/ipsecCreateProfile.png" alt="그림" style="width: 200px;"/>

CLI에서 IPSec 프로파일을 작성하려면 다음 구문을 사용하십시오. 
  
  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra
  
  ```
