---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"

keywords: faq, faqs, questions, vpx, options, ipv6, traffic, network, ha, ssl, vpn

subcollection: citrix-netscaler-vpx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.vpx_full}} 的常見問題
{: #faqs-for-citrix-netscaler-vpx}

下列是使用 {{site.data.keyword.vpx_full}} 時的常見問題。

## 何謂 {{site.data.keyword.vpx_full}}？
{: faq}

Citrix NetScaler 是一種應用程式遞送控制器，可藉由提升效能、確保應用程式可用性及保護，並大幅降低作業成本，讓應用程式效能提高 5 倍。選擇符合應用程式需求的最佳 Citrix NetScaler 發行版本，並針對效能需求，將它部署至適當的專用系統。若要進一步瞭解 Citrix NetScaler，請參閱 Citrix 網站上的 [NetScaler 頁面 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){:new_window}。

## 為何需要負載平衡？
{: faq}

負載平衡資料流量已成為許多客戶實作中的重要層面，因為它會將應用程式要求及負載分散至多部伺服器。它還為整體拓蹼提供了許多優點，包括：

* 安全。根據 IP 通訊協定及埠號，建立應用程式伺服器的邏輯隔離，或拒絕資料流量要求。
* 高可用性。內容會抄寫至儲存區或伺服器群組，保證其可供主機使用。
* 可調整性。其他伺服器會隨著需求的增加而增加，讓負載平衡器將工作負載分散至其他伺服器。
* 效率。配置負載平衡時，會動態分散工作負載。例如，資源（如 CPU）可以更有效率地使用。

## {{site.data.keyword.BluSoftlayer_notm}} 中提供多少個負載平衡選項？
{: faq}

如需 IBM© Load Balancer 供應項目的詳細比較，請參閱[探索負載平衡器](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)。

## NetScaler 是否支援 IPv6？
{: faq}

是。在 {{site.data.keyword.BluSoftlayer_notm}} 公用網路上，同時支援 IPv6 及 IPv4。

## NetScaler 會對專用網路上的資料流量進行負載平衡嗎？
{: faq}

是，NetScaler 是唯一可擴充至專用網路的 {{site.data.keyword.BluSoftlayer_notm}} 負載平衡產品。

## NetScaler 是否可以配置成報告用戶端的來源 IP 位址，而非 NetScaler 應用裝置的來源 IP？
{: faq}

是，在 NetScaler Advanced Management Interface 內，**使用來源 IP (USIP)** 參數可以設為**是**，以容許報告用戶端的來源 IP，而非 NetScaler 的來源 IP。

在應用裝置上啟用 USIP 位址模式，可讓應用裝置在與伺服器進行通訊時，彈性使用 IP 標頭中提供的用戶端 IP 位址。藉由啟用此模式，應用裝置會開啟與用戶端 IP 位址的伺服器連線，也會在重複使用連線時考量用戶端 IP 位址。因此，此模式會根據用戶端 IP 位址，協助每個用戶端的限制使用。

## 在 HA 配置的節點之間，用來交換 HA 相關資訊的各種埠有哪些？
{: faq}

埠 3010，用於同步化及指令傳播。UDP 埠 3003，用來交換活動訊號封包。

## NetScaler VPX 的哪一個版本包括廣域伺服器負載平衡 (GSLB)？
{: faq}

Platinum。

## 在 HA 配置中可以使用 NetScaler 嗎？
{: faq}

是，NetScaler VPX 應用裝置支援「高可用性 (HA)」配置。

NetScaler VPX 伺服器不具備援功能，除非以 HA 模式與夥伴一起配置。作為備份及回復策略的一部分，在使用 NetScaler VPX 時，強烈建議部署 HA 環境。

為其他軟硬體元件提供備援也十分重要。例如，電源供應器及本端磁碟機可能不具備援功能。這些元件的故障可能會導致資料流失。

## {{site.data.keyword.BluSoftlayer_notm}} NetScaler 供應項目是否包括 SSL VPN 功能？
{: faq}

是，此特性稱為 NetScaler Gateway™，而且內含在所有版本中。如需此特性的相關資訊，請造訪 [Citrix 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.citrix.com/products/netscaler-adc/){: new_window}
