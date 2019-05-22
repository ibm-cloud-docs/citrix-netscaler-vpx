---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX ソフトウェア・アプライアンスの使用開始
{: #getting-started}

{{site.data.keyword.BluSoftlayer_notm}}  ソリューションに Citrix NetScaler VPX をデプロイすると、Web アプリケーションの配信が加速され、パフォーマンスが向上するとともに、クラウド・アプリケーションとサービスが最適化されて、使用可能でセキュアな状態に維持されます。 ゲーム、ビッグデータ、分析、プライベート・クラウドといった困難なワークロードがある場合でも、Citrix NetScaler VPX は、ユーザーが最も必要とするタイミング、場所、方法でソリューションを実現できるよう寄与します。

## 始める前に
Citrix NetScaler VPX を開始するには、以下の情報を確認する必要があります。

* お客様の IBM© Cloud カスタマー・ポータルのログイン情報
* ロード・バランサーのデプロイメントの場所
* お客様のニーズに最適な Netscaler タイプ (詳しくは、[ロード・バランサーの探索](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)を参照してください)
* 必要なパブリック IP アドレスの数
* ロード・バランサーの割り当て先となる VLAN

## Citrix NetScaler VPX の注文

Citrix NetScaler VPX ソフトウェア・アプライアンスを注文するには、カスタマー・ポータルの注文ページに移動します。

1. ブラウザーから[「カスタマー・ポータル」![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){: new_window}を開き、ご使用のアカウントにログインします。
2. カスタマー・ポータルのナビゲーションで**「デバイス (Devices)」>「デバイス・リスト (Devices List)」**を選択し、**「デバイスの発注 (Order Device)」**リンクをクリックします。
3. **「SoftLayer 製品およびサービスの注文 (Order SoftLayer Products and Services)」**ページで「ネットワーク (Network)」セクションまでスクロールダウンし、Citrix NetScaler VPX の下の**「注文 (Order)」**リンクをクリックします。
4. Citrix NetScaler VPX ソフトウェア・アプライアンスをデプロイするロケーションをドロップダウン・メニューから選択します。  
5. ソフトウェア・エディション、ソフトウェア・バージョン、およびスループットのニーズに最適な NetScaler タイプを選択します。
6. 必要なパブリック IP アドレスの数を選択します。  
	これらは、NetScaler VPX に仮想 IP アドレス (VIP) としてデプロイされる静的パブリック IP アドレスです。
7. **「続行 (Continue)」**をクリックします。
8. 要求した IP アドレスの ARIN (または、デプロイメント領域内の同等の組織) に必要な情報を入力します。
9. 連絡先情報を入力します。
10. ご使用の VLAN を選択します。
	待ち時間を最小化し、ネットワーク・リソースの使用効率を最適化するには、トラフィックが分散されるサーバーと同じ VLAN に Citrix NetScaler VPX を割り当てます。
11. オーダーを確認し、ご利用条件に同意した上で、**「注文の実行 (Place Order)」**をクリックします。 Citrix NetScaler VPX ソフトウェア・アプライアンスが、選択した設定でデプロイされます。

## 次に行うこと

Citrix Netscaler VPX [フィーチャー](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-about-citrix-netscaler-vpx)の詳細や特定の Netscaler [用語](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-citrix-netscaler-vpx-terminology)を確認したり、お客様の Netscaler の[構成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-basic-load-balancing-configuration)を開始したりできます。
