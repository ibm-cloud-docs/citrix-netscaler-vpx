---

copyright:
  years: 2019
lastupdated: "2019-04-28"

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

# 建立以原則為基礎的遞送 (PBR)
{: #creating-policy-based-routing}

要指定 VPN 將使用的唯一資料流量參數（例如，本端和遠端子網路），需要以原則為基礎的遞送 (PBR) 原則。若要建立 PBR 設定檔，請執行下列步驟：

1.	導覽至**系統 > 網路 > PBR**，然後選取**新增**。
2.	輸入**名稱**。
3.	將**動作**保留為預設設定**容許**。
4.	對於**下一個躍點類型**，選取 **IP 通道**，然後從 **IP 通道名稱**下拉清單中，挑選[先前建立](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel)的通道。
5.	確保已勾選**啟用 PBR**。
6.	在**配置 IP** 區段中，同時對來源和目的地，為**作業**欄位選取 **=**。
7.	在下列欄位中指定第一個和最後一個子網路 IP：
  *	**來源 IP 低位**
  *	**來源 IP 高位**
  *	**目的地 IP 低位**
  *	**目的地 IP 高位**
8.	按一下**建立**。

    <img src="images/ipseCreatePBR1.png" alt="圖片" style="width: 200px;"/>

9.	從**系統 > 網路 > PBR** 中，選取新 PBR，按一下**選取動作**清單，然後選取**套用**。

    <img src="images/ipsecCreatePBR2.png" alt="圖片" style="width: 600px;"/>

若要在 CLI 中建立 PBR 設定檔，請使用下列語法：

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs
  
  ```
  {: codeblock}

  請注意，任何想要透過 VPN 通道並位於 VPX 後面的虛擬伺服器實例或基礎架構，都需要配置為使用 VPX 作為預設閘道或使用靜態路徑。這會在目的地為遠端（同層級）子網路時，將資料流量傳送至 VPX。請參閱下面的靜態路徑 (**10.115.0.0/16**) 範例。
  {: note}

  ```
  >route print
  ===========================================================================
  Interface List
  3...06 93 7a 03 f0 b3 ......XenServer PV Network Device #0
  4...06 ff 8f 6d 89 e8 ......XenServer PV Network Device #1
  1...........................Software Loopback Interface 1
  7...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
  10...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
  ===========================================================================
  
  IPv4 Route Table
  ===========================================================================
  Active Routes:
  Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0    169.54.255.65    169.54.255.73     26
       10.115.0.0      255.255.0.0      192.168.0.1      192.168.0.2     26
  
  ```
  {: codeblock}
