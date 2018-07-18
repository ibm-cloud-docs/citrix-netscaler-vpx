---
copyright:
  years: 1994, 2017
  
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 Citrix NetScaler VPX 軟體應用裝置

在 {{site.data.keyword.BluSoftlayer_notm}} 解決方案中部署 Citrix NetScaler VPX 可加速 Web 應用程式遞送、提高效能，並確保雲端應用程式及服務保持最佳化、可用與安全。如果您有具挑戰性的工作負載（例如遊戲、海量資料與分析或專用雲端），Citrix NetScaler VPX 可協助您依使用者最需要的時間、地點及方式提供解決方案。

## 開始之前
若要開始使用 Citrix NetScaler VPX，您將需要知道下列資訊：

* 您的 IBM Cloud 客戶入口網站登入資訊
* 負載平衡器的部署位置
* 何種 Netscaler 類型最適合您的需要（如需相關資訊，請參閱[探索負載平衡器](https://console.bluemix.net/docs/infrastructure/loadbalancer-service/explore-load-balancers.html)） 
* 需要的公用 IP 位址數目
* 您要指派負載平衡器的 VLAN

## 訂購 Citrix NetScaler VPX

若要訂購 Citrix NetScaler VPX 軟體應用裝置，請導覽至「客戶入口網站」中的訂單頁面：

1. 從瀏覽器中，開啟[客戶入口網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window} 並登入您的帳戶。
2. 在「客戶入口網站」導覽中，選取**裝置 > 裝置清單**，然後按一下**訂購裝置**鏈結。 
3. 在**訂購 SoftLayer 產品及服務**頁面中，向下捲動至「網路」區段，然後按一下 Citrix NetScaler VPX 下的**訂購**鏈結。
4. 從下拉功能表中，選取您要部署 Citrix NetScaler VPX 軟體應用裝置的「位置」。  
5. 選取最適用於您的軟體發行、軟體版本及傳輸量需求的 NetScaler 類型。 
6. 選取您需要的公用 IP 位址數目。  
	這些是靜態公用 IP 位址，部署為 NetScaler VPX 上的虛擬 IP 位址 (VIP)。
7. 按一下**繼續**。
8. 輸入您所要求 IP 位址的 ARIN（或您部署地區中的對等組織）所需的資訊。
9. 輸入您的聯絡資訊。 
10. 選取 VLAN。若要將延遲最小化，並確保將網路資源的使用最佳化，請將 Citrix NetScaler VPX 指派給與將在其中配送資料流量之伺服器的相同 VLAN。 
11. 檢閱訂單，接受條款，然後按一下**下訂單**。Citrix NetScaler VPX 軟體應用裝置會使用您選取的設定進行部署。 

## 下一步為何？

您可以進一步瞭解 Citrix Netscaler VPX [特性](about-citrix-netscaler-vpx.html)、檢閱特定的 Netscaler [術語](terminology.html)，或開始[配置](netscaler-basic-configuration.html)您的 Netscaler。
