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

# DNS レコードの確認と構成
{: #check-and-configure-the-dns-record}

このステップバイステップの例では、IBM© Cloud Internet Services の DNS サービスを使用して、DNS ゾーンとそのレコードを管理します。 このケースでは、使用する FQDN に対してレコードが作成されることを確認する必要があります。 レコードは、Citrix Netscaler VPX 仮想サーバーに構成されるパブリック・アドレスを指す必要があります。

<img src="images/12-add-record.png" alt="図面" style="width: 700px;"/>

Citrix VPX に使用する静的パブリック IP は、カスタマー・ポータルの**「デバイス」>「デバイス・リスト」**にナビゲートして、ご使用の Citrix Netscaler VPX の名前を選択することによって取得できます。

<img src="images/13-check-ip.png" alt="図面" style="width: 300px;"/>
