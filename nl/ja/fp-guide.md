---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: proxy, traffic, appliance

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

# {{site.data.keyword.vpx_full}} アプライアンスを使用したフォワード・プロキシー・トラフィックのリダイレクトの構成
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

このガイドでは、{{site.data.keyword.vpx_full}} アプライアンスを使用してフォワード・プロキシーのセットアップをステップバイステップで構成する方法を説明します。 この構成は、11.1 のソフトウェア・バージョン (Platinum Feature Edition) を実行中の {{site.data.keyword.vpx_full}} アプライアンスと 10Mbps パフォーマンスでテスト済みです。

<img src="images/fp1.png" alt="図面" style="width: 600px;"/>

## このガイドで達成できること
{: #what-you-ll-accomplish}

このステップバイステップ・ガイドでは、サービスを構成する方法を学ぶことができます。

タスク  | 説明
------------- | -------------
[{{site.data.keyword.vpx_full}} の注文](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) | まず、{{site.data.keyword.vpx_full}} アプライアンスを注文します。
[プライベート・サブネットの要求](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) | ご使用のアカウント用のプライベート・サブネットを IBM© サポートに要求してください。
[キャッシュのリダイレクト機能とロード・バランシング機能の有効化](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) | 起点プールやヘルス・チェック・メカニズムなど、アプリケーションのリソースを識別します。
[DNS 仮想サーバーの構成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) | DNS リゾルバーを追加し、DNS サービス・グループを定義してから、DNS 仮想サーバーを定義します。
[HTTP(S) トラフィック用のキャッシュのリダイレクトの構成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic) | HTTP または HTTPS トラフィックを使用して、フォワード・プロキシー仮想サーバー用にキャッシュのリダイレクトを構成します。
[SSL トラフィック用のキャッシュのリダイレクトの構成 (オプション)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) | HTTP または HTTPS の代わりに SSL トラフィックを使用して、フォワード・プロキシー仮想サーバー用にキャッシュのリダイレクトを構成します。
[アウトバウンド・トラフィック用のソース NAT の構成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) | {{site.data.keyword.vpx_full}} アプライアンスを使用して、ご使用のクライアント・マシンからのアウトバウンド・トラフィックで NAT を実行します。
[クライアント・マシンのインターネット・ブラウザーでのプロキシー設定の更新 (オプション)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) | 必要であれば、クライアント・マシンのインターネット・ブラウザーを使用してプロキシー設定を更新してください。
