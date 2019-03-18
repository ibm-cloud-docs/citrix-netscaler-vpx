---



copyright:
  years: 2017
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 配置 SSL 資料流量的快取重新導向（選用）
{: #configure-cache-redirection-for-ssl-traffic-optional-}

您可能想要定義虛擬伺服器來處理 SSL 資料流量，而不為具有 HTTP 或 HTTPS 通訊協定的虛擬伺服器定義快取重新導向（如前一個步驟所述）。 

若要這樣做，請遵循下列步驟：

1. 移至**資料流量管理 > 快取重新導向 > 虛擬伺服器**，然後按一下**新增**。指定正向 Proxy 虛擬伺服器的名稱、選取 SSL 通訊協定和**正向**快取類型。為它指派一個來自您專用子網路的 IP 位址，以及其必備條件埠。 

	<img src="images/fp14.png" alt="圖片" style="width: 300px;"/>

	按一下**確定**。 
	
2. 檢閱摘要頁面，並按一下**確定**以便繼續。
3. 指定「重新導向」、「DNS 虛擬伺服器」及「目的地虛擬伺服器」配置。 
4. 按一下**進階設定**畫面下的**憑證**，以檢視與 SSL 憑證相關的配置。 
5. 按一下空白欄位**無伺服器憑證**。
6. 從「選取伺服器憑證」下拉清單，選取 SSL 伺服器。
7. 視需要輸入憑證配置資訊。

	<img src="images/fp15.png" alt="圖片" style="width: 400px;"/>

	按一下**安裝**。
	
8. 選取**連結**。

	<img src="images/fp16.png" alt="圖片" style="width: 300px;"/>
