---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, dns, security, check, configure

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

# 檢查及配置 DNS 記錄
{: #check-and-configure-the-dns-record}

在此逐步作業範例中，IBM© Cloud Internet Services 中的 DNS 服務是用來管理 DNS 區域及其記錄。在此情況下，您必須確定已針對要使用的 FQDN 建立記錄。記錄應該指向 Citrix Netscaler VPX 虛擬伺服器中配置的公用位址。

<img src="images/12-add-record.png" alt="圖片" style="width: 700px;"/>

可透過導覽至**裝置 > 裝置清單**，然後選取 Citrix Netscaler VPX 的名稱，從「客戶入口網站」擷取要與 Citrix VPX 搭配使用的靜態公用 IP。

<img src="images/13-check-ip.png" alt="圖片" style="width: 300px;"/>
