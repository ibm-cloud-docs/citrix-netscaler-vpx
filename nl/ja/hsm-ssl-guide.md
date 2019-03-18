---

copyright:
  years: 2018
lastupdated: "2018-11-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Citrix Netscaler VPX での SSL オフロードの構成とチューニング
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

このステップバイステップでは、Citrix Netscaler VPX での SSL オフロードの構成とチューニングに関するガイドを提供します。これは、HSM リンクを介して生成される証明書および暗号資料を使用して行います。

**注:** このステップバイステップは、[IBM Hardware Security Module (HSM) と Citrix Netscaler VPX とのデプロイメントおよび構成 (Deploying and Configuring the IBM© Hardware Security Module (HSM) with Citrix Netscaler VPX)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) のステップを完了し、VPX/HSM ペアを注文および作成したことを前提としています。

## デプロイメントについて
このデプロイメントは、以下のコンポーネント仕様でビルドおよびテストされました。

| NetScaler VPX のバージョンとビルド	| HSM ソフトウェアのバージョン | HSM ファームウェアのバージョン | HSM クライアントのバージョン |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: ビルド 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## 論理トポロジー
以下の図は、SSL オフロード・ユース・ケースのネットワーク・トラフィック・フローを示しています。 これは、Citrix VPX と HSM アプライアンスとの間のトラスト・リンクおよび構成の視覚的側面と論理的側面を提供します。

<img src="images/network-flows-logical-topology.jpg" alt="図面" style="width: 700px;"/>

SSL オフロードに精通していない場合は、この [Citrix 記事 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window} を参照してください。

## このガイドで達成できること

このステップバイステップ・ガイドでは、Citrix Netscaler VPX 用に SSL を構成する方法について学ぶことができます。

タスク  | 説明
------------- | -------------
[証明書のインストール](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) |以前の [ステップバイステップ](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx)で作成した SSL 証明書をインストールします。
[DNS レコードの確認と構成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | Citrix Netscaler VPX で仮想サーバーとして構成するパブリック・アドレスを指す FQDN の DNS レコードが存在することを確認します。
[SSL 仮想サーバーの追加と構成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | SSL 仮想サーバーを追加し、構成します。
[新規の暗号スイートの作成と適用](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | AEAD、ECDHE、および ECDSA を優先順位付けおよび優先する暗号スイートを作成します。

## 追加リソース
以下の追加リソースは、IBM Hardware Security Module を使用するときに、Citrix Netscaler VPX を最大限に活用することに役立ちます。

* [NetScaler 12.1 製品資料 (NetScaler 12.1 Product Documentation) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Gemalto サポート・ポータル (Gemalto Support Portal) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [IBM Cloud サポート](https://{DomainName}/docs/get-support?topic=get-support-using-avatar){:new_window}
