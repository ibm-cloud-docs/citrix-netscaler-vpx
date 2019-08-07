---

copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: dns, cache, virtual server

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

# 配置 DNS 虛擬伺服器
{: #configure-the-dns-virtual-server}

若要配置 DNS 虛擬伺服器，請執行下列動作：

1. 移至**資料流量管理 > 負載平衡 > 伺服器**。
2. 按一下「新增」，以新增兩個 IBM© SoftLayer DNS 解析器 - 10.0.80.11 和 10.0.80.12。

	<img src="images/fp5.png" alt="圖片" style="width: 200px;"/> <img src="images/fp5b.png" alt="圖片" style="width: 200px;"/>

3. 接著，透過移至**資料流量管理** > **負載平衡** > **服務群組**並選取**新增**，來建立及定義 DNS 服務群組。

	<img src="images/fp6.png" alt="圖片" style="width: 400px;"/>

4. 選取 DNS 通訊協定，然後按一下**確定**。

	<img src="images/fp7.png" alt="圖片" style="width: 300px;"/>

5. 在下一個畫面中，先按一下**服務群組成員**下的空白欄位，將新的 DNS 解析器新增為這個 DNS 服務群組的成員伺服器。

6. 從「建立服務群組成員」畫面，指定 DNS 埠 53，然後按一下「建立」。

	<img src="images/fp8.png" alt="圖片" style="width: 200px;"/>

7. 按一下「關閉」，然後按一下「完成」。

	假設您可以從 {{site.data.keyword.vpx_full}} 應用裝置呼叫到兩個 IBM SoftLayer DNS 解析器，服務群組即會顯示為綠色。

8. 現在，請移至「資料流量管理」>「負載平衡」>「虛擬伺服器」，然後按一下「新增」以定義 DNS 虛擬伺服器。
9. 在「基本設定」下，提供虛擬伺服器的名稱、選擇 DNS 通訊協定及埠 53，然後從專用子網路指派 IP 位址。

	<img src="images/fp9.png" alt="圖片" style="width: 300px;"/>

10. 在接下來的頁面上，按一下標籤為**無負載平衡虛擬伺服器服務群組連結**的空欄位。
11. 從下拉清單選取您先前定義的 DNS 服務群組，然後按一下「連結」。  

	<img src="images/fp10.png" alt="圖片" style="width: 300px;"/>

12. 按一下「繼續」，然後按一下「完成」。

您的 DNS 虛擬伺服器狀態現在應該顯示為綠色。

<img src="images/fp11.png" alt="圖片" style="width: 500px;"/>
