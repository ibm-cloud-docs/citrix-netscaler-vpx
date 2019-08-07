---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security

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

# 使用 {{site.data.keyword.vpx_full}} 來部署和配置 IBM Hardware Security Module (HSM)
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

此逐步作業會引導您整合 HSM 與 {{site.data.keyword.vpx_full}}。然後，這兩個服務將能夠通訊及產生建立憑證所需的加密資料。

## 關於部署
{: #about-the-deployment}
此部署已使用下列元件規格進行建置及測試：

|NetScaler VPX 版本 & 建置|HSM 軟體版本|HSM 韌體版本|HSM 用戶端版本|
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

如果您擁有更早版本的 VPX，或者如果透過 IBM© Cloud 平台訂購裝置時僅看到 11.1 版和更舊版本作為選擇選項，則可升級裝置，以便讓本手冊中所述的設定可以完成。
{: note}

## 邏輯拓蹼
{: #logical-topology}
下圖顯示 SSL 卸載使用案例的網路資料傳輸流。這會提供 VPX 與 HSM 應用裝置之間的信任鏈結及配置的視覺化及邏輯視景。

<img src="images/network-flows-logical-topology.jpg" alt="圖片" style="width: 700px;"/>

如果您不熟悉 SSL 卸載，請檢閱這篇 [Citrix 文章](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html)。

## 您將達成的目標

{: #what-you-ll-accomplish}

在此逐步作業手冊中，您將學習如何使用 {{site.data.keyword.vpx_full}} 來部署及配置 HSM：

 作業 |說明
------------- | -------------
[訂購 Hardware Security Module (HSM)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) |首先，您需要訂購 HSM。
[訂購 {{site.data.keyword.vpx_full}}](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) |如果您還沒有的話，請訂購 {{site.data.keyword.vpx_full}}。
[起始設定 HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) |大部分配置需要起始設定 HSM 裝置。若沒有，則只能執行某些 `show` 指令。
[建立分割區](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition)|分割區是一種邏輯且獨立的空間，它關聯於或連接在 HSM 引擎中要求或建立加密物件的用戶端。
[安裝 HSM 用戶端軟體](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software)|在這個子節中，VPX 將隨著與 HSM 互動所需的軟體和公用程式一起安裝。|
[建立網路信任鏈結 (NTL)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) |「網路信任鏈結 (NTL)」是 Hardware Security Module (HSM) 和用戶端通訊用的安全通道。|
[建立金鑰並產生憑證簽署要求 (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) |在這個子節中，我們將建立一個金鑰組，以用來產生「憑證簽章要求 (CSR)」，並用它訂購/要求憑證。|
[訂購憑證](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) |為 {{site.data.keyword.vpx_full}} 訂購 SSL 憑證。
[擷取及移轉憑證](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) |擷取先前訂購的 SSL 憑證，然後在下個逐步作業中，讓一切備妥以進行安裝與配置。
