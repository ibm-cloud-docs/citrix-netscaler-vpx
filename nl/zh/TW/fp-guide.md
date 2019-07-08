---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: proxy, traffic, appliance

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

# 使用 Citrix NetScaler VPX 應用裝置配置正向 Proxy 資料流量重新導向
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

本手冊為您提供逐步作業配置，以便使用 Citrix NetScaler VPX 應用裝置進行正向 Proxy 設定。此配置是在執行軟體版本 11.1（白金級特性版本）及 10Mbps 效能的 Citrix NetScaler VPX 應用裝置上測試的。

<img src="images/fp1.png" alt="圖片" style="width: 600px;"/>

## 您將達成的目標
{: #what-you-ll-accomplish}

在此逐步作業手冊中，您將學習如何部署服務：

 作業 |說明
------------- | -------------
[訂購 Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) |首先訂購 Citrix NetScaler VPX 應用裝置。
[要求專用子網路](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) |從「IBM© 支援中心」為您的帳戶要求專用子網路。
[啟用快取重新導向及負載平衡功能](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) |識別應用程式的資源，例如原點儲存區和性能檢查機制。
[配置 DNS 虛擬伺服器](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) |新增您的 DNS 解析器、定義 DNS 服務群組，然後定義 DNS 虛擬伺服器。
[配置 HTTP(S) 資料流量的快取重新導向](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic) |為具有 HTTP 或 HTTPS 資料流量的正向 Proxy 虛擬伺服器配置快取重新導向。
[配置 SSL 資料流量的快取重新導向（選用）](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) |為具有 SSL 資料流量而非 HTTP 或 HTTPS 的正向 Proxy 虛擬伺服器配置快取重新導向。
[配置出埠資料流量的來源 NAT](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) |利用 Citrix NetScaler VPX 應用裝置，對來自您用戶端機器的出埠資料流量執行 NAT。
[在用戶端機器的網際網路瀏覽器上更新 Proxy 設定（選用）](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) |使用用戶端機器的網際網路瀏覽器來更新 Proxy 設定（如果需要的話）。
