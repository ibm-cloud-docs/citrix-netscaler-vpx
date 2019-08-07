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

# 在 {{site.data.keyword.vpx_full}} 中使用 IBM Virtual Router Appliance 置配置 IPSec 站台對站台 VPN
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

本手冊提供了在 Citrix VPX 中配置 IPSec VPN 站台對站台連線的逐步指示。IBM Virtual Router Appliance (VRA) 用作 VPN 同層級。

<img src="images/ipsec1.png" alt="圖片" style="width: 600px;"/>

## 關於部署
此部署已使用下列元件規格進行建置及測試：

|NetScaler VPX 版本 & 建置|VRA 版本和說明| 
| ------------- | ------------- | 
| NS12.1: Build 48.13.nc |AT&T vRouter 5600 1801q|

您需要 VPX Platinum 授權才能配置 IPSec VPN。
{: note}

## 開始之前

本手冊假定擁有這兩個裝置。請造訪下列鏈結以取得訂購的指示。

-	[開始使用 {{site.data.keyword.vpx_full}} 軟體應用裝置](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[開始使用 IBM Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## 您將達成的目標

在本手冊中，您將瞭解如何在 Citrix VPX 裝置中配置 IPSec VPN。

 作業 |說明
------------- | -------------
[啟用 VPX 中的必要特性](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx)|首先，啟用必要的特性來建立 IPSec VPN。
[建立 IPSec 設定檔](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile)|IPSec 設定檔包含用於建立連線的安全參數。
[建立 IP 通道](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel)|在此章節中，我們會建立 IP 通道物件來同時指定本端和遠端 IP 位址，以及通訊協定參數。
[建立以原則為基礎的遞送 (PBR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing)|PBR 是用來同時定義本端和遠端子網路的唯一資料流量參數。
[配置 VRA](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra)|使用對等的 VPN 配置語法來配置 Virtual Router Appliance。
[驗證 VPN 狀態](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection)|驗證 VPN 作業狀態並處理簡單的連線功能測試。

## 其他資源
下列其他資源可協助您進一步瞭解 Citrix VPX 和 Virtual Router Appliance 的相關資訊。

* [CloudBridge Connector ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configuring a CloudBridge Connector tunnel between a Citrix ADC appliance and Cisco IOS device ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Citrix VPX/ADC 12.1 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [補充 VRA 文件](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
