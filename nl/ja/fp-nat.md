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

# アウトバウンド・トラフィック用のソース NAT の構成
{: #configure-source-nat-for-outbound-traffic}

ネットワーク・アドレス変換 (NAT) は、トラフィック・ルーティング・デバイスでの転送中にパケットの IP ヘッダー内のネットワーク・アドレス情報を変更することで、1 つの IP アドレス・スペースを別の IP アドレス・スペースに再マップする方法です。

{{site.data.keyword.vpx_full}} アプライアンスを使用して、ご使用のクライアント・マシンからのアウトバウンド・トラフィックで NAT を実行できます。 構成するには、以下の手順に従ってください。

1. 「システム」 > 「ネットワーク」 > 「経路」と移動し、**「RNAT」**タブにナビゲートします。 **「RNAT の構成 (Configure RNAT)」**をクリックします。

2. RNAT を適用したいソース・サブネット (およびマスク) を指定して、**「OK」**をクリックします。

このサブネットで任意の IP から送信されるインターネットへのトラフィックが、Citrix NetScaler のパブリック IP アドレス上のトラフィックで NAT を使用するようになりました。    
