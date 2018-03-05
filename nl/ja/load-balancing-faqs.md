---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

<a name="top"></a>
# FAQ

Citrix NetScaler VPX を使用する際のよくある質問を以下に示します。

## Citrix NetScaler VPX とは何ですか?

Citrix NetScaler はアプリケーション・デリバリー・コントローラーです。パフォーマンスの促進、アプリケーションの可用性と安全性の確保、運用コストの大幅な削減を通じて、アプリケーションを 5 倍良好にします。アプリケーションの要件を満たす最適な Citrix NetScaler エディションを選択し、パフォーマンスのニーズに応じて適切な専用システムにデプロイします。Citrix NetScaler について詳しくは、Citrix Web サイトの[「NetScaler ページ」![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){: new_window}を参照してください。

## なぜ、ロード・バランシングが必要なのですか?

ロード・バランシング・トラフィックは、アプリケーションの要求と負荷を複数のサーバーに分散するため、多くのお客様の実装で重要な側面になりました。また、トポロジー全体にも以下に示すように多数の利点があります。

* セキュリティー。アプリケーション・サーバーが論理的に分離されるか、IP プロトコルとポート番号に基づいてトラフィック要求が拒否されます。
* 高可用性。コンテンツはプール (サーバーのグループ) に複製され、ホストに可用性が保証されます。
* 拡張容易性。必要に応じてサーバーを追加することが可能で、ロード・バランサーによって追加のサーバーにワークロードを分散できます。
* 効率性。ロード・バランシングが構成されると、ワークロードは動的に分散されます。例えば、CPU などのリソースをより効率的な方法で使用できます。

## {{site.data.keyword.BluSoftlayer_notm}} で使用可能なロード・バランシング・オプションの数を教えてください

IBM のロード・バランサー・オファリングの詳細な比較については、[「ロード・バランサーの探索」](https://dev-console.bluemix.net/docs/infrastructure/loadbalancer-service/explore-load-balancers.html#explore-load-balancers)を参照してください。

## NetScaler は IPv6 をサポートしますか?

はい。{{site.data.keyword.BluSoftlayer_notm}} パブリック・ネットワークでは、IPv6 と IPv4 の両方がサポートされます。

## NetScaler はプライベート・ネットワーク上のトラフィックのロード・バランシングを行いますか?

はい。NetScaler はプライベート・ネットワークに拡張される唯一の {{site.data.keyword.BluSoftlayer_notm}} ロード・バランシング製品です。

## NetScaler アプライアンスのソース IP ではなく、クライアントのソース IP アドレスを報告するように NetScaler を構成できますか?

はい。NetScaler 詳細管理インターフェース (Advanced Management Interface) 内で**「ソース IP を使用 (Use Source IP (USIP))」**パラメーターを **「はい (YES)」**に設定することで、NetScaler ではなくクライアントのソース IP を報告するようにできます。

アプライアンスで USIP アドレス・モードを有効にすると、IP ヘッダーで使用可能なクライアント IP アドレスをサーバーとの通信時に使用でき、アプライアンスの柔軟性が高まります。このモードを有効にすると、アプライアンスはクライアント IP アドレスを使用してサーバー接続を開き、接続の再使用時にもクライアント IP アドレスを考慮します。したがって、このモードにより、クライアント IP アドレスに基づくクライアントごとの制限付き再使用が容易になります。

## HA 構成のノード間で HA 関連の情報を交換するには、どのポートが使用されますか?

同期およびコマンド伝搬用に、ポート 3010 です。ハートビート・パケット交換用に、UDP ポート 3003 です。

## どのバージョンの NetScaler VPX にグローバル・サーバー・ロード・バランシング (GSLB) が含まれていますか?

Platinum です。

## NetScaler を HA 構成に含めることはできますか?

はい。NetScaler VPX アプライアンスは高可用性 (HA) 構成をサポートします。

NetScaler VPX サーバーは、パートナーと HA モードで構成されていない限り、冗長ではありません。バックアップとリカバリー戦略の一部として、NetScaler VPX の使用時には HA 環境をデプロイすることを強くお勧めします。

他のハードウェアとソフトウェア・コンポーネントに対して冗長性を提供することも重要です。例えば、電源装置やローカル・ディスク・ドライブに冗長性がない場合があります。このようなコンポーネントで障害が発生すると、データが失われる可能性があります。

## {{site.data.keyword.BluSoftlayer_notm}} NetScaler オファリングには、SSL VPN 機能が搭載されていますか?

はい。この機能は NetScaler Gateway ™ と呼ばれ、すべてのエディションに組み込まれています。この機能について詳しくは、[「Citrix の Web サイト」![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.citrix.com/products/netscaler-adc/){: new_window}を参照してください。
