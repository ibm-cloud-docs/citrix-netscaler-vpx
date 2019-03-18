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

# 擷取及移轉憑證
{: #retrieve-and-transfer-the-certificate}

擷取先前訂購的 SSL 憑證，以便您能夠在下個「逐步作業」[使用 Citrix Netscaler VPX 配置及調整 SSL 卸載](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx)。

1. 在驗證網域的所有權之後不久，您應該會收到一封電子郵件，確認已完成憑證履行和憑證本身。

	複製從 `---BEGIN CERTIFICATE---` 一直到 `---END CERTIFICATE---` 的文字，並將內容儲存為新的憑證檔案，使用副檔名 `.cer`。

2. 將憑證檔案複製到 Citrix Netscaler VPX 中的 `/nsconfig/ssl` 目錄。

<img src="images/11-transfer-certificate.png" alt="圖片" style="width: 600px;"/>

Citrix Netscaler VPX 現在已準備好將憑證併入使用 SSL 的負載平衡部署中。
