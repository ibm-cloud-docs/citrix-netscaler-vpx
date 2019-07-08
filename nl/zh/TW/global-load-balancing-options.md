---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: gslb, vpx, cdn, object storage

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 廣域負載平衡
{: #global-load-balancing}

廣域伺服器負載平衡 (GSLB) 是一種將資料流量分割到使用 DNS 及地理位置的多部伺服器的方法，以作為判斷應傳送伺服器資料流量之位置的手段。一般而言，廣域負載平衡器會將用戶端要求傳送至較接近用戶端的伺服器，以減少延遲並改善效能。

您可能不需要完整實作廣域負載平衡解決方案。GSLB 需要多個可執行此功能的合適裝置實例，而且取決於您的需求，其他解決方案可能會更吸引您。如果您需要整個網站及應用程式，則 GSLB 是良好的選擇。如果您只需要內容的某些部分（例如影像、視訊或其他大型檔案），則[內容遞送網路](/docs/infrastructure/CDN?topic=CDN-about-content-delivery-networks-cdn-)可能更為適合（更容易部署）。

## Citrix NetScaler VPX
{: #citrix-netscaler-vpx}

Citrix NetScaler VPX 是唯一能夠執行真正廣域負載平衡的客戶可配置裝置。NetScaler 是可執行 DNS 型廣域負載平衡查閱的多功能應用裝置。您可以指向 NetScaler 以作為 DNS 伺服器，而且裝置將會檢查它配置成負載平衡的伺服器、執行距離計算，以及傳回具有最接近用戶端要求之伺服器 IP 的記錄。

對於適用於負載平衡，您會在每個資料中心都有 NetScaler 應用裝置配置。每個 NetScaler 應用裝置配置可以是單一 Netscaler 或一對 HA 配對的 Netscaler，視您的需求而定，它們會為背後的伺服器提供本端負載平衡服務。裝置已配置為彼此交談，以在指派給廣域負載平衡器旋轉的每一部伺服器上交換狀態資訊。任何進入這些已配置 NetScaler 的 DNS 要求都可以傳回在線上且具回應力之伺服器的適當記錄。任何沒有回應的伺服器都會從旋轉及另一個選取項目中移除。

您必須已設定負載平衡，即使它是唯一在進行平衡的伺服器。您需要一些服務的額外 IP 位址，即 GSLB 網站 IP。NetScaler 使用此 IP 與廣域負載平衡通訊協定中的其他 NetScaler 進行通訊。

下列廣域平衡程序使用：

### VPX1
{: #vpx1}

`50.97.235.236` 的名稱為 `VPX1Vserver`，是該裝置的本端負載平衡 VIP。`50.23.66.52` 將稱為 `VPX1site`，是該裝置之 GSLB 的本端 IP。

### VPX2
{: #vpx2}
`208.43.241.249` 用於 `VPX2Vserver`，而 GSLB IP 是 `208.43.224.4`，稱為 `VPX2site`。

1. 移至**資料流量管理 > GSLB**，然後按一下滑鼠右鍵以啟用此特性。然後，選取**網站**及**新增**。

2. 在第一個裝置上，將「名稱」輸入為 VPX1、將「類型」輸入為 local，並將 IP 輸入為 `50.23.66.52`，然後選取**關閉**。

	您應該會看到狀態列為綠色的網站。還不要新增遠端網站。

3. 移至**資料流量管理 > GSLB**，然後選取 **GSLB 精靈**。按**下一步**。輸入將進行負載平衡的主機名稱（在此範例中為 `gslb.tsstesting.com`）。將「記錄類型」保留為 A，且將「服務類型」保留為 ANY。虛擬伺服器名稱會自行移入資料。按**下一步**。

4. 選擇您的平衡形式及持續性方法，就像使用一般負載平衡一樣。按**下一步**。

5. 網站已移入資料，因此您不需要新增任何項目。請改為按一下第一個網站名稱旁的綠色 '+'。從清單中選取該裝置上的 Vserver，然後按一下**建立**。您應該會看到該網站已配置了網站 IP 以及負載平衡設定的 Vserver IP，並且該網站為綠色。按**下一步**、**完成**及**結束**。

6. 使用該伺服器的值，對下一個 NetScaler 執行相同的動作。

7. 在這兩部伺服器上，移至**資料流量管理 > DNS > 記錄 > A 記錄**，然後檢查清單。您應該會看到類型為 `GSLB 網域`的 `root.servers.net` 項目，以及主機名稱。

8. 移至**資料流量管理 > DNS > 名稱伺服器**，然後按一下**新增**。在 NetScaler 上輸入 IP 位址（例如，裝置的公用 IP）。按一下**本端**，讓通訊協定保留為 UDP。按一下**建立**，然後按一下**關閉**。您應該會看到有效狀態為已啟用並已執行。

9. 移至**系統 > 網路 > IP**，然後開啟 GSLB IP 位址。請確定已為這兩部機器選取**管理**。

10. 接下來，在這兩部伺服器上，回到**資料流量管理 > GSLB**，然後再次執行精靈。此時，請按**下一步**，然後選取**修改現有網域的配置**。從清單中選取主機名稱，然後按兩次**下一步**。

11. 在網址欄位中，放入另一個 NetScaler 的網站 IP 位址，並提供另一個 NetScaler 的網站名稱，然後按一下**新增**。網站將移入可再按一次綠色 '+' 的選項。按一下遠端網站加號，以新增另一個網站。輸入 Vserver 服務 IP（負載平衡伺服器的相應 IP，而不是 GSLB 網站 IP）和埠，按一下**建立** > **關閉** > **下一步** > **完成**，然後按一下**結束**。

如果所有項目都已執行到這個點，而且兩部伺服器都已配置，則「GSLB 虛擬伺服器」、「服務」及「網站」中所有項目的狀態都應該是綠色。您會發現兩部機器的 GSLB 服務中現在有兩個項目（如果已適當同步化）。此時，伺服器現在會彼此通訊。

您現在必須配置 DNS。

在 `gslb.tsstesting.com` 範例中，您會在 tsstesting.com 區域中建立 NS 及中介記錄：

    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; nameserver IP of first NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; nameserver IP of second NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias to the GSLB object on the NetScaler appliance

請記住，您只能使用 CNAME 與主機名稱搭配，而不是網域的根目錄。

此配置會將 `gslb.tsstesting.com` 要求的名稱伺服器，設為您已在其上配置 DNS 的 NetScaler IP。CNAME 記錄會將 `tsstesting.com` 轉換成 `gslb.tsstesting.com` 的要求。然後，`www.tsstesting.com` 的任何要求都會移至要解析的 NetScaler，並且會根據您所配置的負載平衡方法傳回記錄。

如需 NetScaler 廣域負載平衡的相關資訊，請參閱：
* [配置 Netscaler 進行廣域負載平衡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://support.citrix.com/article/CTX110348){: new_window}
* [在 NetScaler 上 DNS（網域名稱系統）如何使用 GSLB 特性 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://support.citrix.com/article/CTX122619){: new_window}
* [MEP 通訊協定及網站監視的相關資訊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://support.citrix.com/article/CTX111081){: new_window}

有其他產品可以提供類似的功能，以根據地理位置來分散資料流量：

### CDN
{: #cdn}

內容遞送網路 (CDN) 容許您將原點伺服器上傳或提供給地理位置不同的快取伺服器，然後將內容提供給發出要求的用戶端。CDN 適用於靜態、大量內容（例如未隨著時間變更的影像及視訊）。

如需 CDN 的詳細資料，請參閱[本文件](/docs/infrastructure/CDN?topic=CDN-getting-started)。

### Object Storage
{: #object-storage}

{{site.data.keyword.BluSoftlayer_notm}} 的 Object Storage 可以配置成使用各種資料中心內的多個地理位置來提供內容。地理位置感知應用程式可以對用戶端要求執行位置查閱，並將 URL 傳回給靠近用戶端的 Object Storage。必要的話，Object Storage 也會隨附 CDN 前端系統，以提供如上述的其他快取服務。

如需 Object Storage 的相關資訊及簡介，請參閱[本文件](/docs/services/cloud-object-storage?topic=cloud-object-storage-about)。
