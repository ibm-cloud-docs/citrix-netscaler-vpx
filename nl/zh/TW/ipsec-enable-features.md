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

# 啟用 Citrix NetScaler VPX 中的必要特性
{: #enable-required-features-in-vpx}

您可以啟用 VPX 中的必要特性來建立 IPSec VPN：

1.	存取 VPX GUI（圖形使用者介面）。
2.	導覽至**系統 > 設定 > 配置模式**，然後啟用**第 3 層模式（IP 轉遞）**。
3.	移至**系統 > 設定 > 配置進階功能**，然後啟用**雲端橋接器**。

若要在 CLI 中啟用這些特性，請執行下列指令：

```
> enable ns feature CloudBridge
> enable ns mode L3

```

如需使用 GUI 或 SSH 連接至 NetScaler 的其他指示，請造訪[下列文章](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler)。
