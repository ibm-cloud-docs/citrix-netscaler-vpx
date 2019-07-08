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

# 创建 IP 隧道
{: #creating-ip-tunnel}

您需要创建 IP 隧道对象，用于指定本地和远程 IP 地址以及 VPN 连接的协议参数。为此，请执行以下操作：

1.	导航至**系统 > CloudBridge Connector > IP 隧道**。
2.	在 **IPv4 隧道**选项卡上，单击**添加**。
3.	输入以下参数：
  *	名称
  *	远程 IP（远程 VPN 同级的 IP）
  *	远程掩码
4.	在“本地 IP”下拉列表中，选择**子网 IP** (SNIP)。
5.	从**本地 IP** 下拉列表中，选择要用作 VPN 端点的相应 SNIP。
6.	从下拉列表中，选择 **IPSEC** 作为协议。
7.	从 **IPSec 概要文件名称**下拉列表中，选择[先前创建](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx)的概要文件名称。 
8.	单击**创建**。

    <img src="images/ipsecCreateIPtunnel.png" alt="图样" style="width: 200px;"/>

要在 CLI 中创建 IP 隧道，请使用以下语法：
  
  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1
  
  ```
