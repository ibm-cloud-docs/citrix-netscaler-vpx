---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: proxy, update

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

# 在用戶端機器的網際網路瀏覽器上更新 Proxy 設定（選用）
{: #update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-}

若要使用用戶端機器的網際網路瀏覽器來更新 Proxy 設定，請執行下列步驟：

1. 移至瀏覽器設定中的**網際網路選項**，將它配置成使用 Proxy 伺服器來處理送出的要求。
2. 使用先前步驟中定義的快取重新導向虛擬伺服器 IP 位址作為 Proxy。

如果 {{site.data.keyword.vpx_full}} 應用裝置位於用戶端機器和網際網路之間的直接第 3 層路徑中，那麼可能不需要這些 Proxy 設定。
{: note}

<img src="images/fp17.png" alt="圖片" style="width: 500px;"/>
