---
copyright:
  years: 1994, 2018
  
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX の最新の更新
{: #recent-updates-for-citrix-netscaler-vpx}

## バージョン 12.1

### 複数の IP アドレスを持つ仮想サーバー
複数の連続しないまたは連続する VIP IPv4 および IPv6 アドレスを持つ単一のロード・バランシング仮想サーバーを作成できるようになりました。 仮想サーバーにバインドされる個々の VIP は、個別の仮想サーバーとして取り扱われます。

この機能について詳しくは、Citrix の記事 [複数 IP の仮想サーバー (Multiple IP virtual servers) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}を参照してください。

### SSL
SSL 接続について、以下の更新が適用されました。
 
* 弱い暗号を DEFAULT_BACKEND 暗号グループから削除。 
* Thales nShield® 外部 HSM のフロントエンドで ECDHE 暗号をサポート。
* SafeNet ネットワークの外部 HSM のフロントエンドで ECDHE 暗号をサポート。
* SSLv2 の削除: NetScaler VPX アプライアンスは、12.1 以降 SSLv2 をサポートしていません。

12.1 の SSL の更新について詳しくは、[Citrix 12.1 リリース・ノート![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}を参照してください。

### GSLB サービス・グループのサポート
GSLB 用の IP アドレス・ベースのサービス・グループ、ドメイン名ベースのサービス・グループ、またはドメイン名ベースのオート・スケール・サービス・グループを構成できるようになりました。 サービスのグループを単一のサービスと同様に簡単に管理したり、仮想サービスにサービス・グループをバインドしたり、グループにサービスを追加したりすることもできます。

GSLB サービス・グループについて詳しくは、Citrix の記事 [GSLB サービス・グループの構成 (Configuring a GSLB service group)![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}を参照してください。
