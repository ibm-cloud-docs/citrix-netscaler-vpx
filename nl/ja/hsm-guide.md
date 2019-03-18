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

# Citrix Netscaler VPX を使用した IBM Hardware Security Module (HSM) のデプロイと構成
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

このステップバイステップ・ガイドは、HSM を Citrix Netscaler VPX と統合するプロセスを説明します。 統合後、この 2 つのサービスは、証明書の作成に必要な暗号素材を通信および生成できるようになります。

## デプロイメントについて
このデプロイメントは、以下のコンポーネント仕様でビルドおよびテストされました。

| NetScaler VPX のバージョンとビルド	| HSM ソフトウェアのバージョン | HSM ファームウェアのバージョン | HSM クライアントのバージョン |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: ビルド 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

**注:** 古いバージョンの VPX をお持ちの場合、もしくは IBM© Cloud プラットフォームでデバイスを注文する際、選択オプションに 11.1 以前のバージョンしか表示されない場合、このガイドで説明するセットアップを完了できるようにデバイスをアップグレードすることができます。 

## 論理トポロジー
以下の図は、SSL オフロード・ユース・ケースのネットワーク・トラフィック・フローを示しています。 これは、VPX アプライアンスと HSM アプライアンスの間のトラスト・リンクおよび構成の、視覚的側面と論理的側面を表しています。 

<img src="images/network-flows-logical-topology.jpg" alt="図面" style="width: 700px;"/>

SSL オフロードに精通していない場合は、この [Citrix 記事](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html)を参照してください。

## このガイドで達成できること

このステップバイステップ・ガイドでは、Citrix Netscaler VPX を使用して HSM をデプロイして構成する方法を学ぶことができます。

タスク  | 説明
------------- | -------------
[Hardware Security Module (HSM) の注文](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) | 最初に、HSM を注文する必要があります。
[Citrix Netscaler VPX の注文](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) | まだ注文していない場合は、Citrix Netscaler VPX を注文します。
[HSM の初期化](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) | ほとんどの構成で HSM デバイスの初期化が必要となります。 これを行わないと、特定の `show` コマンド以外は実行できません。 
[パーティションの作成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition) | パーティションとは、HSM エンジン内で暗号オブジェクトを要求または作成するクライアントに関連付けまたは接続された論理スペースまたは独立スペースです。
[HSM クライアント・ソフトウェアのインストール](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software) | このサブセクションでは、HSM との相互作用で必要となるソフトウェアおよびユーティリティーと共に VPX がインストールされます。 |
[ネットワーク・トラスト・リンク (NTL) の確立](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) |ネットワーク・トラスト・リンク (NTL) は Hardware Security Module (HSM) および通信するクライアントのセキュア・チャネルです。|
[鍵の作成および証明書署名要求 (CSR) の生成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) | このサブセクションでは、証明書署名要求 (CSR) の生成に使用される鍵ペアを作成し、それを使用して証明書を注文または要求します。 | 
[証明書の注文](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) | Citrix Netscaler VPX の SSL 証明書を注文します。
[証明書の取得と転送](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) | 先ほど注文した SSL 証明書を取得し、次のステップバイステップでのインストールと構成に備えて準備します。 
