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

# {{site.data.keyword.vpx_full}} の必須機能の有効化
{: #enable-required-features-in-vpx}

VPX で IPSec VPN を作成するための必須機能を有効にすることができます。

1.	VPX の GUI (グラフィカル・ユーザー・インターフェース) にアクセスします。
2.	**「System」>「Settings」>「Configure Modes」**とナビゲートし、**「Layer 3 Mode (IP Forwarding)」**を有効にします。
3.	**「System」>「Settings」>「Configure Advanced Features」**と移動し、**「Cloud Bridge」**を有効にします。

CLI でこれらの機能を有効にするには、以下のコマンドを実行します。

```
> enable ns feature CloudBridge
> enable ns mode L3

```

GUI または SSH を使用して NetScaler に接続する方法について詳しくは、[次の記事](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler)を参照してください。
