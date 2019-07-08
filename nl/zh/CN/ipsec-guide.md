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

# 在 Citrix NetScaler VPX 中使用 IBM 虚拟路由器设备配置 IPSec 站点到站点 VPN
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

本指南提供了在 Citrix VPX 中配置 IPSec VPN 站点到站点连接的逐步指示信息。IBM 虚拟路由器设备 (VRA) 用作 VPN 同级。

<img src="images/ipsec1.png" alt="图样" style="width: 600px;"/>

## 关于部署
此部署是使用以下组件规范进行构建和测试的：

|NetScaler VPX 版本和构建|VRA 版本和描述| 
| ------------- | ------------- | 
|NS12.1：构建 48.13.nc|AT&T vRouter 5600 1801q|

您需要 VPX Platinum 许可证才能配置 IPSec VPN。
{: note}

## 开始之前

本指南假定拥有这两个设备。请访问以下链接以获取有关订购的指示信息。

-	[Citrix NetScaler VPX 软件设备入门](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[IBM 虚拟路由器设备入门](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## 需要完成的任务

在本指南中，您将了解如何在 Citrix VPX 设备中配置 IPSec VPN。

任务|描述
------------- | -------------
[启用 VPX 中的必需功能](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx)|首先，启用必需的功能来创建 IPSec VPN。
[创建 IPSec 概要文件](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile)|IPSec 概要文件包含用于建立连接的安全参数。
[创建 IP 隧道](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel)|在此部分中，将创建 IP 隧道对象，用于指定本地和远程 IP 地址以及协议参数。
[创建基于策略的路由 (PBR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing)|PBR 用于定义本地和远程子网的唯一流量参数。
[配置 VRA](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra)|使用等效的 VPN 配置语法来配置虚拟路由器设备。
[验证 VPN 状态](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection)|验证 VPN 操作状态并执行简单的连接测试。

## 其他资源
以下其他资源可帮助您了解有关 Citrix VPX 和虚拟路由器设备的更多信息。

* [CloudBridge Connector ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configuring a CloudBridge Connector tunnel between a Citrix ADC appliance and Cisco IOS device ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Citrix VPX/ADC 12.1 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [补充 VRA 文档](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
