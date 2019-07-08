---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, configure, configuration, http, traffic

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

# 配置 HTTP(S) 資料流量的快取重新導向
{: #configure-cache-redirection-for-http-traffic}

若要配置 HTTP 或 HTTPS 資料流量的快取重新導向，請遵循下列步驟：

1. 移至**資料流量管理 > 快取重新導向 > 虛擬伺服器**，然後按一下**新增**。
2. 指定正向 Proxy 虛擬伺服器的名稱。從各自的下拉清單中，選取 **HTTP** 通訊協定和**正向**快取類型。然後，將 IP 位址從專用子網路指派給此虛擬伺服器。

	<img src="images/fp12.png" alt="圖片" style="width: 300px;"/>

	按一下**確定**以便繼續。

3. 檢閱摘要頁面，並按一下**確定**。  
4. 按一下**資料流量設定**，以檢視其他配置設定。
5. 根據您的需求，從「資料流量設定」選取下列三個重新導向選項之一：
	* **快取** - 將所有出埠要求導向至本端快取伺服器儲存區。
	* **原則** - 檢查快取重新導向原則，以判斷該要求應該轉遞至快取伺服器儲存區，還是目的地伺服器（原點）。
	* **原點** - 將所有出埠要求導向至各自的目的地伺服器（原點）。

6. 從下拉清單 **DNS 虛擬伺服器名稱**，選取先前配置的 DNS 虛擬伺服器，並將**重新導向**選項設定為**原點**。

	<img src="images/fp13.png" alt="圖片" style="width: 300px;"/>

	**附註：**當要將出埠資料流量導向至本端快取伺服器儲存區時，會使用**目的地虛擬伺服器**設定。當您想要將所有出埠資料流量導向至原點伺服器時，請將其留空。

7. 按一下**確定**，然後按一下**完成**。
