---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, security, add, configure

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

# 新增及配置 SSL 虛擬伺服器
{: #add-and-configure-the-ssl-virtual-server}

若要新增及配置 SSL 虛擬伺服器，請執行下列程序：

1. 導覽至**系統 > 設定 > 配置基本特性**。選取 **SSL 卸載**，然後按一下**確定**。
2. 在 NetScaler GUI 中，導覽至**資料流量管理 > 負載平衡 > 服務 > 新增**，並指定名稱、IP 位址，並將通訊協定設為 **HTTP**。按一下**確定**完成。
3. 確認服務可正常作業：

	<img src="images/15-confirm-service.png" alt="圖片" style="width: 700px;"/>

4. 對任何其他伺服器重複步驟 2。
5. 導覽至**資料流量管理 > 負載平衡 > 虛擬伺服器**，然後按一下**新增**。指定名稱，並選取 **SSL** 作為通訊協定，然後輸入公用 IP 位址。按一下**確定**完成。
6. 現在，選取**無負載平衡虛擬伺服器服務連結**，然後按一下**選取**。選取您在先前步驟中建立的服務、按一下「選取」，然後按一下**連結/繼續**。

	<img src="images/18-bind-service.png" alt="圖片" style="width: 700px;"/>

7. 最後，按一下**無伺服器憑證**、按一下**選取伺服器憑證**，然後選取先前安裝的憑證。按一下**選取**、**連結/繼續**，然後按一下**完成**來完成。
