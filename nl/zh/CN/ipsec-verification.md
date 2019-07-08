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

# 验证 VPN 隧道连接
{: #verifying-vpn-tunnel-connection}

执行以下过程和命令来验证 VPN 连接的运行状态：

1.	通过导航至**系统 > CloudBridge Connector > IP 隧道**来确认 VPX 中的 VPN 状态。

  <img src="images/ipsecVerifyVPN1.png" alt="图样" style="width: 600px;"/>

  “状态”应该在相应的 IP 隧道条目（在此示例中为 **IPSec_tunnel1**）中反映 **UP** 状态。

  要使用 CLI 确认 VPN 连接的状态，请运行以下命令：

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

2.	通过在 CLI 中执行以下命令来确认 VPN 状态，以确认 VRA 中的 VPN 状态：
    
  ```
  $ show vpn ipsec sa
  Peer ID / IP                            Local ID / IP
  ------------                            -------------
  10.143.220.106                          10.115.168.144
  
  Tunnel  Id          State  Bytes Out/In   Encrypt       Hash      DH A-Time  L-Time
  ------  ----------  -----  -------------  ------------  --------  -- ------  ------
  1       1           up     0.0/0.0        aes256        sha1      2  18466   86400
  ```

  3.	通过从 Citrix VPX 后面的 VSI 向远程（虚拟路由器设备）端的 VSI 发出 ping 操作，以测试 VPN 连接：

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
