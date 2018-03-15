---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 存取及管理 Citrix NetScaler VPX

Citrix NetScaler 裝置是功能強大的工具，具有許多特性可協助您透過多種方式來加強及調整 {{site.data.keyword.BluSoftlayer_notm}} 解決方案。您可以在「客戶入口網站」中找到裝置的資訊，以及連接至裝置並配置其特性。  

## 在客戶入口網站中尋找 NetScaler 詳細資料

Citrix NetScaler 裝置會列在「裝置清單」中，就像您在 {{site.data.keyword.BluSoftlayer_notm}} Platform 上具有的任何其他伺服器。

若要尋找「裝置清單」，請執行下列動作：

1. 從瀏覽器中，開啟[客戶入口網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window}，並登入您的帳戶。
2. 在「客戶入口網站」導覽中，選取**裝置 > 裝置清單**。

您將會看到依裝置名稱排序的裝置。Citrix NetScaler VPX 裝置的「裝置類型」為 "NetScaler"。 

在 NetScaler 列的左側，按一下箭頭來展開該行，並顯示用於 NetScaler 管理存取的使用者名稱及遮罩過的密碼。 

「裝置清單」中列出的其他詳細資料，包括： 

* 位置（NetScaler 所在的資料中心）
* 專用 IP 位址（其用來連接至 NetScaler 以進行管理功能）
* 開始日期（訂購及佈建機器時）

**附註：**雖然入口網站中列出 NetScaler 的「專用 IP 位址」，但是未列出 NetScaler 的「公用 IP 位址」。原因是使用「專用 IP 位址」管理 NetScaler，並且使用 NetScaler 裝置的「公用 IP 位址」作為裝置的 VIP 或「虛擬 IP」，而這些項目用於負載平衡服務。

## 裝置詳細資料畫面 

按一下 NetScaler 的名稱會帶領您前往 NetScaler 的**裝置詳細資料**頁面，該頁面會顯示已部署 NetScaler 的 VLAN，以及 NetScaler 的「公用 IP 位址」。這些 IP 位址無法用於進行管理，因為它們是 NetScaler 的預設「公用 VIP 位址」。稍後，您將使用這些 IP 位址來建立與「服務」的關聯，以達到負載平衡目的。

## 管理 NetScaler

{{site.data.keyword.BluSoftlayer_notm}} 授與對 NetScaler 裝置的完整 root 存取權。若要登入 NetScaler 的「管理使用者介面」，您必須連接至 {{site.data.keyword.BluSoftlayer_notm}} 專用網路（{{site.data.keyword.BluSoftlayer_notm}} 管理 VPN，或從 {{site.data.keyword.BluSoftlayer_notm}} 環境之伺服器上的遠端階段作業執行管理功能）。 

若要從「客戶入口網站」連接至 NetScaler 的「管理使用者介面」，請按一下**裝置詳細資料**畫面右上角的**動作**下拉清單，然後選擇**管理裝置**，以在瀏覽器中啟動新的標籤或蹦現視窗。這會將您遞送至 NetScaler 的 NSIP（您先前所看到的「專用 IP 位址」）。顯示的頁面會要求裝置的 root 使用者名稱及密碼。一旦輸入資訊之後，即會帶領您前往「NetScaler 管理 GUI」。 

或者，您可以將 NetScaler 裝置的專用 IP 複製並貼入 Web 瀏覽器。

### NetScaler SSH 存取

您也可以使用慣用的 SSH 用戶端，直接連接至 NetScaler 裝置。從「裝置清單」頁面中使用 NetScaler 裝置的「專用 IP」及登入資訊，並確定您已連接至 {{site.data.keyword.BluSoftlayer_notm}} VPN。 
