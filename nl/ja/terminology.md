---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: terminology, nsip, snip, vip, service, object, monitor

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.vpx_full}} 用語
{: #citrix-netscaler-vpx-terminology}

Citrix NetScaler プラットフォームは、製品固有の用語と基本的なロード・バランサーの用語および概念を使用しています。

### NetScaler IP (NSIP)
{: #netscaler-ip-nsip-}

管理目的で指定されたロード・バランサーの IP。

### SubNet IP (SNIP)
{: #subnet-ip-snip-}

SNIP は、NetScaler がサーバー (またはオブジェクト) と通信しようとするたびに使用するパケットのソース IP アドレスです。 また、サーバーも NetScaler に応答するために SubNet IP を使用します。

### 仮想 IP (VIP)
{: #virtual-ip-vip-}

VIP は、クライアントが要求を送信する IP アドレスです。 NetScaler は VIP でのクライアント接続を終了し、ロード・バランシング・サービスに構成されたサーバーとの接続を開始します。  これは、パブリック (インターネット) トラフィック用のパブリック IP アドレス、またはプライベート (イントラネット) トラフィック用のプライベート IP アドレスのいずれかになります。

### 仮想サーバー
{: #virtual-server}

ロード・バランシング用語での仮想サーバーとは、IP クライアントの接続先であり、NetScaler によってロード・バランシングされている特定のアプリケーションのトラフィック要求が送信される場所である、IP アドレス、ポート、およびプロトコルの組み合わせを指します。

### サービス
{: #service}

要求を特定のサーバーに経路指定するために使用される IP アドレス、ポート、およびプロトコルの組み合わせ。 サービスは、構成後、仮想サーバーに関連付ける必要があります。

### サーバー・オブジェクト
{: #server-object}

通常の IP アドレスを使用するのではなく、意味のある名前を物理サーバーに割り当てることができる仮想エンティティー。

### モニター
{: #monitor}

サービスを追跡し、サービスが正しく作動していることを確認できるようにするエレメント。 モニターは、プローブおよびハートビート信号を使用してサービス状況を追跡します。
