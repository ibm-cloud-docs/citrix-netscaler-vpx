---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: nat, traffic, configure, configuration

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

# 配置出埠資料流量的來源 NAT
{: #configure-source-nat-for-outbound-traffic}

網址轉換 (NAT) 是一種將 IP 位址空間重新對映至另一個 IP 位址空間的方法，重新對映的方法是在封包在資料流量遞送裝置之間傳輸時，修改封包之 IP 標頭中的網址資訊。

您可以利用 Citrix NetScaler VPX 應用裝置，對來自您用戶端機器的出埠資料流量執行 NAT。若要這麼做，請執行下列動作：

1. 移至「系統」>「網路」>「路徑」，然後導覽至 **RNAT** 標籤。按一下**配置 RNAT**。

2. 指定您要套用 RNAT 的來源子網路（及遮罩），然後按一下**確定**。

源自此子網路中任何 IP 且送往網際網路的資料流量，現在將針對 Citrix NetScaler 公用 IP 位址上的資料流量使用 NAT。    
