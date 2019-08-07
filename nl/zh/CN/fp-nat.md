---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: nat, traffic, configure, configuration

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

# 为出站流量配置源 NAT
{: #configure-source-nat-for-outbound-traffic}

网络地址转换 (NAT) 是一种 IP 地址空间重新映射方法，通过修改在流量路由设备中传输的包的 IP 头中的网络地址信息，将一个 IP 地址空间重新映射到另一个 IP 地址空间。

您可利用 {{site.data.keyword.vpx_full}} 设备从客户端机器对出站流量执行 NAT。为此，请执行以下操作：

1. 转至“系统”>“网络”>“路径”，然后浏览至 **RNAT** 选项卡。单击**配置 RNAT**。

2. 指定要应用 RNAT 的源子网（和掩码），然后单击**确定**。

现在，源自此子网中任何 IP 的因特网绑定流量都将对 Citrix NetScaler 的公共 IP 地址上的流量使用 NAT。    
