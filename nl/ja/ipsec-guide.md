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

# Citrix NetScaler VPX と IBM Virtual Router Appliance による IPSec サイト間 VPN の構成
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

このガイドでは、Citrix VPX で IPSec VPN サイト間の接続を構成する手順をステップバイステップで説明します。IBM Virtual Router Appliance (VRA) は VPN ピアとして使用されます。

<img src="images/ipsec1.png" alt="図" style="width: 600px;"/>

## デプロイメントについて
このデプロイメントは、以下のコンポーネント仕様でビルドおよびテストされました。

| NetScaler VPX のバージョンとビルド	| VRA バージョン & 説明 | 
| ------------- | ------------- | 
| NS12.1: ビルド 48.13.nc | AT&T vRouter 5600 1801q |

IPSec VPN を構成するには、VPX Platinum ライセンスが必要です。
{: note}

## 始める前に

このガイドは両方のデバイスを所有していることを前提としています。注文方法については、以下のリンクにアクセスしてください。

-	[Citrix NetScaler VPX ソフトウェア・アプライアンスの使用開始](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[IBM Virtual Router Appliance の概要](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## このガイドで達成できること

このガイドでは、Citrix VPX デバイスで IPSec VPN を構成する方法について学ぶことができます。

タスク  | 説明
------------- | -------------
[
VPX の必須機能の有効化](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) | まずは、IPSec VPN を作成するための必須機能を有効にします。
[
IPSec プロファイルの作成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile) | IPSec プロファイルには、接続を確立するためのセキュリティー・パラメーターが含まれています。
[
IP トンネルの作成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) | このセクションでは、ローカルとリモートの両方の IP アドレスおよびプロトコル・パラメーターを指定するための IP トンネル・オブジェクトを作成します。
[ポリシー・ベース・ルーティング (PBR) の作成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing) | PBR は、ローカル・サブネットとリモート・サブネットの両方に固有のトラフィック・パラメーターを定義するために使用します。
[VRA の構成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra) |Virtual Router Appliance を、同等の VPN 構成の構文を使用して構成します。
[VPN のステータスの確認](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection) | VPN の動作状態を確認し、簡単な接続テストを実施します。

## 追加リソース
Citrix VPX と Virtual Router Appliance についてさらに理解したい場合は、以下の追加リソースが役に立ちます。

* [CloudBridge Connector ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configuring a CloudBridge Connector tunnel between a Citrix ADC appliance and Cisco IOS device ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Citrix VPX/ADC 12.1 の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [VRA の補足資料](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
