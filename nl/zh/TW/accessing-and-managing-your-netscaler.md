---
copyright:
  years: 1994, 2019

lastupdated: "2019-06-11"

keywords: manage, managing, locating, details, portal, device, list

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 管理 Citrix NetScaler VPX
{: #managing-your-citrix-netscaler-vpx}

Citrix NetScaler 裝置是功能強大的工具，具有許多特性可協助您透過多種方式來加強及調整 {{site.data.keyword.cloud}} 解決方案。您可以在 {{site.data.keyword.cloud_notm}} 基礎架構客戶入口網站中找到該裝置的資訊，還可以連接至該裝置並配置其特性。  

## 在客戶入口網站中找到 NetScaler 詳細資料
{: #locating-netscaler-details-in-the-customer-portal}

Citrix NetScaler 裝置列在「裝置清單」中，這與您在 {{site.data.keyword.cloud_notm}} 平台上擁有的其他任何伺服器一樣。

若要尋找「裝置清單」，請執行下列動作：

1. 從您的瀏覽器開啟[客戶入口網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window} 並登入到您的帳戶。
2. 在客戶入口網站導覽中，選取**裝置 > 裝置清單**。

您將會看到依裝置名稱排序的裝置。Citrix NetScaler VPX 裝置的「裝置類型」為 "NetScaler"。

在 NetScaler 列的左側，按一下箭頭來展開該行，並顯示用於 NetScaler 管理存取的使用者名稱及遮罩過的密碼。

「裝置清單」中列出的其他詳細資料，包括：

* 位置（NetScaler 所在的資料中心）
* 專用 IP 位址（其用來連接至 NetScaler 以進行管理功能）
* 開始日期（訂購及佈建機器時）

入口網站中列出了 NetScaler 的專用 IP 位址，但並未列出 NetScaler 的公用 IP 位址。原因是使用「專用 IP 位址」管理 NetScaler，並且使用 NetScaler 裝置的「公用 IP 位址」作為裝置的 VIP 或「虛擬 IP」，而這些項目用於負載平衡服務。
{: note}

## 裝置詳細資料畫面
{: #the-device-details-screen}

按一下 NetScaler 的名稱會帶領您前往 NetScaler 的**裝置詳細資料**頁面，該頁面會顯示已部署 NetScaler 的 VLAN，以及 NetScaler 的「公用 IP 位址」。這些 IP 位址無法用於進行管理，因為它們是 NetScaler 的預設「公用 VIP 位址」。稍後，您將使用這些 IP 位址來建立與負載平衡服務的關聯。

## 連接至 NetScaler
{: #connecting-to-the-netscaler}

{{site.data.keyword.cloud_notm}} 授與對 NetScaler 裝置的完整 root 存取權。若要登入 NetScaler 的「管理使用者介面」，您必須連接至 {{site.data.keyword.cloud_notm}} 專用網路（{{site.data.keyword.BluSoftlayer_notm}} 管理 VPN，或從 {{site.data.keyword.cloud_notm}} 環境之伺服器上的遠端階段作業執行管理功能）。

若要從客戶入口網站連接至 NetScaler 的管理使用者介面，請按一下**裝置詳細資料**畫面右上角的**動作**下拉清單，然後選擇**管理裝置**以在瀏覽器中啟動新標籤或蹦現視窗。這會將您遞送至 NetScaler 的 NSIP（您先前所看到的「專用 IP 位址」）。顯示的頁面會要求裝置的 root 使用者名稱及密碼。一旦輸入資訊之後，即會帶領您前往「NetScaler 管理 GUI」。

或者，您可以將 NetScaler 裝置的專用 IP 複製並貼入 Web 瀏覽器。

### NetScaler SSH 存取
{: #netscaler-ssh-access}

您也可以使用慣用的 SSH 用戶端，直接連接至 NetScaler 裝置。從「裝置清單」頁面中使用 NetScaler 裝置的「專用 IP」及登入資訊，並確定您已連接至 {{site.data.keyword.cloud_notm}} VPN。
