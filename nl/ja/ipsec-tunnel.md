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

# IP トンネルの作成
{: #creating-ip-tunnel}

ローカルとリモートの IP アドレスだけでなく、VPN 接続のプロトコル・パラメーターを指定するためにも、IP トンネル・オブジェクトを作成する必要があります。構成するには、以下の手順に従ってください。

1.	**「System」>「CloudBridge Connector」>「IP Tunnels」**とナビゲートします。
2.	**「IPv4 Tunnels」**タブで、**「Add」**をクリックします。
3.	次のパラメーターを入力します。
  *	Name
  *	Remote IP (リモート VPN ピアの IP)
  *	Remote Mask
4.	**「Subnet IP」**(SNIP) を「Local IP」ドロップダウン・リストで選択します。
5.	VPN エンドポイントとして使用する適切な SNIP を**「Local IP」**ドロップダウンから選択します。
6.	プロトコルとして、ドロップダウン・リストから**「IPSEC」**を選択します。
7.	**「IPSec Profile Name」**ドロップダウンから、[前に作成した](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx)プロファイル名を選択します。 
8.	**「Create」**をクリックします。

    <img src="images/ipsecCreateIPtunnel.png" alt="図" style="width: 200px;"/>

CLI で IP トンネルを作成するには、次の構文を使用します。
  
  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1
  
  ```
