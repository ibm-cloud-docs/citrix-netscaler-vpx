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

# 创建基于策略的路由 (PBR)
{: #creating-policy-based-routing}

要指定 VPN 将使用的唯一流量参数（例如，本地和远程子网），需要基于策略的路由 (PBR) 策略。要创建 PBR 概要文件，请执行以下步骤：

1.	导航至**系统 > 网络 > PBR**，然后选择**添加**。
2.	输入**名称**。
3.	将**操作**保留为缺省设置**允许**。
4.	对于**下一个中继段类型**，选择 **IP 隧道**，然后从 **IP 隧道名称**下拉列表中，选取[先前创建](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel)的隧道。
5.	确保已选中**启用 PBR**。
6.	在**配置 IP** 部分中，对于源和目标，为**运算**字段选择 **=**。
7.	在以下字段中指定第一个和最后一个子网 IP：
  *	**源 IP 低位**
  *	**源 IP 高位**
  *	**目标 IP 低位**
  *	**目标 IP 高位**
8.	单击**创建**。

    <img src="images/ipseCreatePBR1.png" alt="图样" style="width: 200px;"/>

9.	从**系统 > 网络 > PBR** 中，选择新 PBR，单击**选择操作**列表，然后选择**应用**。

    <img src="images/ipsecCreatePBR2.png" alt="图样" style="width: 600px;"/>

要在 CLI 中创建 PBR 概要文件，请使用以下语法：

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs
  
  ```
  {: codeblock}

  请注意，任何旨在通过 VPN 隧道并位于 VPX 后面的虚拟服务器实例或基础架构，都需要配置为使用 VPX 作为缺省网关或使用静态路由。这将在目标是远程（同级）子网时，向 VPX 发送流量。请参阅下面的静态路由 (**10.115.0.0/16**) 示例。
  {: note}

  ```
  >route print
  ===========================================================================
  Interface List
  3...06 93 7a 03 f0 b3 ......XenServer PV Network Device #0
  4...06 ff 8f 6d 89 e8 ......XenServer PV Network Device #1
  1...........................Software Loopback Interface 1
  7...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
  10...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
  ===========================================================================
  
  IPv4 Route Table
  ===========================================================================
  Active Routes:
  Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0    169.54.255.65    169.54.255.73     26
       10.115.0.0      255.255.0.0      192.168.0.1      192.168.0.2     26
  
  ```
  {: codeblock}
