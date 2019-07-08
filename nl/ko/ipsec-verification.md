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

# VPN 터널 연결 확인
{: #verifying-vpn-tunnel-connection}

다음 프로시저와 명령을 실행하여 VPN 연결의 작동 상태를 확인할 수 있습니다. 

1.	**시스템 > CloudBridge 커넥터 > IP 터널**로 이동하여 VPX의 VPN 상태를 확인하십시오. 

  <img src="images/ipsecVerifyVPN1.png" alt="그림" style="width: 600px;"/>

  상태는 개별 IP 터널 항목(이 예에서 **IPSec_tunnel1**)의 **UP** 상태를 반영해야 합니다. 

  CLI를 사용하여 VPN 연결의 상태를 확인하려면 다음 명령을 실행하십시오.

  ```    
  > show iptunnel
  1) 도메인.......:               0
    이름.........:  IPSec_tunnel1 (TUN1)
    원격.......:  10.115.168.144   마스크......: 255.255.255.255
    로컬........:  10.143.220.106   Encap.....:  10.143.220.106
    프로토콜.....:           IPSEC   유형......:               C
    IPSec 프로파일 이름.......:  IPSec_Profile1
    IPSec 터널 상태......:              UP
    PBR 수..........:               1

    Done
      
  ```

2.	VPN 상태를 확인하려면 CLI에서 다음 명령을 실행하여 VRA의 VPN 상태를 확인하십시오.
    
  ```
  $ show vpn ipsec sa
  피어 ID / IP                            로컬 ID / IP
  ------------                            -------------
  10.143.220.106                          10.115.168.144

  터널     Id          상태  바이트 출력/입력   암호화           해시      DH A-Time  L-Time
  ------  ----------  -----  -------------  ------------  --------  -- ------  ------
  1       1           up     0.0/0.0        aes256        sha1      2  18466   86400
  ```

  3.	Citrix VPX 뒤의 VSI에서 원격(가상 라우터 어플라이언스) 측의 VSI로 ping을 실행하여 VPN 연결을 테스트하십시오.

  ```
  >ping 10.115.72.237
  
  32바이트의 데이터로 10.115.72.237 Ping 실행:
  10.115.72.237의 응답: 바이트=32 시간=37ms TTL=63
  10.115.72.237의 응답: 바이트=32 시간=36ms TTL=63
  10.115.72.237의 응답: 바이트=32 시간=35ms TTL=63
  10.115.72.237의 응답: 바이트=32 시간=35ms TTL=63

  10.115.72.237의 Ping 통계:
      패킷: 전송 = 4, 수신 = 4, 유실 = 0(0% 손실),
  개략적인 라운드트립 시간(밀리초):
      최소 = 35ms, 최대 = 37ms, 평균 = 35ms
  ```
