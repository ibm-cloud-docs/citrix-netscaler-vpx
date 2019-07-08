---

copyright:
  years: 2019
lastupdated: "2019-04-08"

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

# 启用 Citrix NetScaler VPX 中的必需功能
{: #enable-required-features-in-vpx}

您可以启用 VPX 中的必需功能来创建 IPSec VPN：

1.	访问 VPX GUI（图形用户界面）。
2.	导航至**系统 > 设置 > 配置方式**，然后启用**第 3 层方式（IP 转发）**。
3.	转至**系统 > 设置 > 配置高级功能**，然后启用**云网桥**。

要在 CLI 中启用这些功能，请执行以下命令：

```
> enable ns feature CloudBridge
> enable ns mode L3

```

有关使用 GUI 或 SSH 连接到 NetScaler 的其他指示信息，请访问[以下文章](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler)。
