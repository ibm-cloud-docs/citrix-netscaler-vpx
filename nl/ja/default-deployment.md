---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-6"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# デフォルトのデプロイメント

[カスタマー・ポータル![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/)の**「デバイス (Devices)」>「デバイス・リスト (Device List)」**で NetScaler を表示すると、他のサーバーとは異なる外観になることがあります。つまり、デバイスにはプライベート IP アドレスはありますが、パブリック IP アドレスはありません。

{{site.data.keyword.BluSoftlayer_notm}} での NetScaler のデフォルト・デプロイメントは、管理目的で使用される NetScaler IP (NSIP) としてプライベート IP アドレスを自動的に割り当てることにより、可能な限りセキュアになるように設計されています。NetScaler の左側にある矢印をクリックすると、行が展開され、デフォルトのユーザー名 (ルート) とマスクされたルート・ユーザー・パスワードが表示されます。 

{{site.data.keyword.BluSoftlayer_notm}} は、プロビジョニング中に多くの決定を処理します。例えば、どの IP アドレスをどの目的で使用するのかなどの決定です。デプロイメントに使用する VLAN をユーザーに問います。また、個別のパブリック VLAN とプライベート VLAN へのインターフェースの割り当てや、NSIP、VIP、SNIPを含む各インターフェースへの適切な IP アドレスの割り当てなど、スクリプトと API を使用してバックエンド構成の多くを自動化します。

## 何を構成する必要があるか?

デフォルトでは、NSIP はプロビジョニング中に割り当てられるプライベート IP アドレスです。これは、管理目的で NetScaler への接続に使用する IP アドレスです。SNIP (SubNet IP アドレス) は、デフォルトでは、順序付けプロセス中に選択した VLAN に存在する同一の 1 次 IP サブネットから割り当てられます。 

目的のロード・バランシング済みサーバーが存在する VLAN と同じ VLAN を選択する場合、これらの SNIP の追加構成は不要です。デフォルトでは、DNS は {{site.data.keyword.BluSoftlayer_notm}} のネーム・サーバーに設定されます。基本的な実装では、ご使用のサーバーの DNS レコードが {{site.data.keyword.BluSoftlayer_notm}} によってホストされる場合、これ以上の構成は不要です。
