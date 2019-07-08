---

copyright:
  years: 2019
lastupdated: "2019-04-10"

keywords: ipsec, vpn, vpx, tunnel

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

# 建立 IP 通道
{: #creating-ip-tunnel}

您需要建立 IP 通道物件，不僅要指定本端和遠端 IP 位址，還要指定 VPN 連線的通訊協定參數。若要這麼做，請執行下列動作：

1.	導覽至**系統 > CloudBridge Connector > IP 通道**。
2.	在 **IPv4 通道**標籤上，按一下**新增**。
3.	輸入下列參數：
  *	名稱
  *	遠端 IP（遠端 VPN 同層級的 IP）
  *	遠端遮罩
4.	在「本端 IP 」下拉清單中，選取**子網路 IP** (SNIP)。
5.	從**本端 IP** 下拉清單中，選擇要用作 VPN 端點的相應 SNIP。
6.	從下拉清單中，選取 **IPSEC** 作為通訊協定。
7.	從 **IPSec 設定檔名稱**下拉清單中，選擇[先前建立](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx)的設定檔名稱。 
8.	按一下**建立**。

    <img src="images/ipsecCreateIPtunnel.png" alt="圖片" style="width: 200px;"/>

若要在 CLI 中建立 IP 通道，請使用下列語法：
  
  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1
  
  ```
