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

# 驗證 VPN 通道連線
{: #verifying-vpn-tunnel-connection}

執行下列程序和指令來驗證 VPN 連線的作業狀態：

1.	通過導覽至**系統 > CloudBridge Connector > IP 通道**來確認 VPX 中的 VPN 狀態。

  <img src="images/ipsecVerifyVPN1.png" alt="圖片" style="width: 600px;"/>

  「狀態」應該在相應的 IP 通道項目（在此範例中為 **IPSec_tunnel1**）中反映 **UP** 狀態。

  若要使用 CLI 確認 VPN 連線的狀態，請執行下列指令：

  ```    
  > show iptunnel
  1) Domain.......:               0
    Name.........:  IPSec_tunnel1 (TUN1)
    Remote.......:  10.115.168.144   Mask......: 255.255.255.255
    Local........:  10.143.220.106   Encap.....:  10.143.220.106
    Protocol.....:           IPSEC   Type......:               C
    IPSec Profile Name.......:  IPSec_Profile1
    IPSec Tunnel Status......:              UP
    Number of PBRs ..........:               1
      
    Done
      
  ```

2.	通過在 CLI 中執行下列指令來確認 VPN 狀態，以確認 VRA 中的 VPN 狀態：
    
  ```
  $ show vpn ipsec sa
  Peer ID / IP                            Local ID / IP
  ------------                            -------------
  10.143.220.106                          10.115.168.144
  
  Tunnel  Id          State  Bytes Out/In   Encrypt       Hash      DH A-Time  L-Time
  ------  ----------  -----  -------------  ------------  --------  -- ------  ------
  1       1           up     0.0/0.0        aes256        sha1      2  18466   86400
  ```

  3.	通過從 Citrix VPX 後面的 VSI 向遠端 (Virtual Router Appliance) 端的 VSI 發出 ping 操作，以測試 VPN 連線功能：

  ```
  >ping 10.115.72.237
  
  Pinging 10.115.72.237 with 32 bytes of data:
  Reply from 10.115.72.237: bytes=32 time=37ms TTL=63
  Reply from 10.115.72.237: bytes=32 time=36ms TTL=63
  Reply from 10.115.72.237: bytes=32 time=35ms TTL=63
  Reply from 10.115.72.237: bytes=32 time=35ms TTL=63
  
  Ping statistics for 10.115.72.237:
      Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
  Approximate round trip times in milli-seconds:
      Minimum = 35ms, Maximum = 37ms, Average = 35ms
  ```
