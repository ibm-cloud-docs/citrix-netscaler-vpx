---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, configure, tune, tuning, ssl, offload

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

# 使用 Citrix Netscaler VPX 配置及調整 SSL 卸載
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

此逐步作業會引導您在 Citrix Netscaler VPX 中配置及調整 SSL 卸載，這可透過使用透過 HSM 鏈結產生的憑證和加密資料來完成。

本逐步作業假定您已完成了[使用 Citrix NetScaler VPX 部署和配置 IBM© Hardware Security Module (HSM)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) 中用於訂購和建立 VPX/HSM 配對的步驟。
{: note}

## 關於部署
{: #about-the-deployment}
此部署已使用下列元件規格進行建置及測試：

|NetScaler VPX 版本 & 建置|HSM 軟體版本|HSM 韌體版本|HSM 用戶端版本|
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## 邏輯拓蹼
{: #logical-topology}

下圖顯示 SSL 卸載使用案例的網路資料傳輸流。這會提供 Citrix VPX 與 HSM 應用裝置之間的信任鏈結及配置的視覺化及邏輯視景。

<img src="images/network-flows-logical-topology.jpg" alt="圖片" style="width: 700px;"/>

如果您不熟悉 SSL 卸載，請檢閱這篇 [Citrix 文章 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}。

## 您將達成的目標
{: #what-you-ll-accomplish}

在此逐步作業手冊中，您將學習如何配置 Citrix Netscaler VPX 的 SSL：

 作業 |說明
------------- | -------------
[安裝憑證](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) |安裝您在前一個[逐步作業](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx)中建立的 SSL 憑證。
[檢查及配置 DNS 記錄](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) |確定 FQDN 的 DNS 記錄存在且指向要在 Citrix Netscaler VPX 中配置為「虛擬伺服器」的公用位址。
[新增及配置 SSL 虛擬伺服器](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) |新增及配置 SSL 虛擬伺服器。
[建立及套用新的密碼組合](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) |建立優先使用且偏好 AEAD、ECDHE 及 ECDSA 的密碼組合。

## 其他資源
{: #additional-resources}
下列其他資源可以協助您在使用 IBM Hardware Security Module 時，充分利用 Citrix Netscaler VPX。

* [NetScaler 12.1 Product Documentation ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Gemalto Support Portal ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [IBM Cloud 支援中心](/docs/get-support?topic=get-support-using-avatar){:new_window}
