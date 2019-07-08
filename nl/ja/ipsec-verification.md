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

# VPN トンネル接続の確認
{: #verifying-vpn-tunnel-connection}

次の手順とコマンドを実行して、VPN 接続の動作ステータスを確認します。

1.	**「System」>「CloudBridge Connector」>「IP Tunnels」**とナビゲートして、VPX で VPN のステータスを確認します。

  <img src="images/ipsecVerifyVPN1.png" alt="図" style="width: 600px;"/>

  各 IP トンネル・エントリー (この例では **IPSec_tunnel1**) の「Status」に **UP** 状態が表されているはずです。

  CLI を使用して VPN 接続のステータスを確認するには、次のコマンドを実行します。

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

2.	VPN の状態を確認する次のコマンドを CLI で実行して、VRA で VPN のステータスを確認します。
    
  ```
  $ show vpn ipsec sa
  Peer ID / IP                            Local ID / IP
  ------------                            -------------
  10.143.220.106                          10.115.168.144
  
  Tunnel  Id          State  Bytes Out/In   Encrypt       Hash      DH A-Time  L-Time
  ------  ----------  -----  -------------  ------------  --------  -- ------  ------
  1       1           up     0.0/0.0        aes256        sha1      2  18466   86400
  ```

  3.	Citrix VPX の背後にある VSI からリモート (Virtual Router Appliance) 側の VSI に ping を発行して、VPN 接続をテストします。

  ```
  >ping 10.115.72.237
  
  10.115.72.237 に ping を送信しています 32 バイトのデータ:
  10.115.72.237 からの応答: バイト数=32 時間=37ms TTL=63
  10.115.72.237 からの応答: バイト数=32 時間=36ms TTL=63
  10.115.72.237 からの応答: バイト数=32 時間=35ms TTL=63
  10.115.72.237 からの応答: バイト数=32 時間=35ms TTL=63

  10.115.72.237 の ping 統計:
      パケット数: 送信 = 4、受信 = 4、損失 = 0 (0% の損失)、
  ラウンド トリップの概算時間 (ミリ秒):
      最小 = 35ms、最大 = 37ms、平均 = 35ms
  ```
