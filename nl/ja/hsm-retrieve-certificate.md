---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, retrieve, transfer, certificate

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

# 証明書の取得と転送
{: #retrieve-and-transfer-the-certificate}

以前に注文した SSL 証明書を取得し、次のステップバイステップ [{{site.data.keyword.vpx_full}} での SSL オフロードの構成とチューニング (Configuring and Tuning SSL Offload with {{site.data.keyword.vpx_full}})](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx) で証明書をインストールおよび構成する準備をします。

1. ドメインの所有権を有効にした直後に、証明書のフルフィルメントの完了を確認する E メールおよび証明書そのものを受信するはずです。

	`---BEGIN CERTIFICATE---` から `---END CERTIFICATE---` までのテキストをコピーし、そのコンテンツを、拡張子 `.cer` の新規の証明書ファイルとして保存します。

2. 証明書ファイルを {{site.data.keyword.vpx_full}} の `/nsconfig/ssl` ディレクトリーにコピーします。

  <img src="images/11-transfer-certificate.png" alt="図面" style="width: 600px;"/>

{{site.data.keyword.vpx_full}} で SSL を使用したロード・バランシング・デプロイメントに証明書を組み込む準備ができました。
