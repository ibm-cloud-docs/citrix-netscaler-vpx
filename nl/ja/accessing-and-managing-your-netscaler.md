---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX の管理
{: #managing-your-citrix-netscaler-vpx}

Citrix NetScaler デバイスは、さまざまな方法で {{site.data.keyword.BluSoftlayer_notm}} ソリューションを拡張および改良するのに役立つ豊富な機能を備えた強力なツールです。 カスタマー・ポータルでデバイスの情報を見ることができるほか、デバイスに接続してそのフィーチャーを構成することもできます。  

## カスタマー・ポータルでの NetScaler の詳細の表示

Citrix NetScaler デバイスは、{{site.data.keyword.BluSoftlayer_notm}} プラットフォーム上にある他のサーバーと同様に、デバイス・リストにリストされます。

デバイス・リストを見つけるには、以下のようにします。

1. ブラウザーから[「カスタマー・ポータル」![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){: new_window}を開き、ご使用のアカウントにログインします。
2. カスタマー・ポータルのナビゲーションで、**「デバイス (Devices)」>「デバイス・リスト (Device List)」**を選択します。

ご使用のデバイスが、デバイス名でソートされて表示されます。 Citrix NetScaler VPX デバイスのデバイス・タイプは「NetScaler」です。 

NetScaler の行の左側で、矢印をクリックして行を展開し、NetScaler 管理アクセス用のユーザー名とマスクされたパスワードを表示します。 

デバイス・リストにリストされるその他の詳細には、以下のものがあります。 

* ロケーション (NetScaler があるデータ・センター)
* プライベート IP アドレス (管理機能を目的として NetScaler に接続するために使用されます)
* 開始日 (マシンが発注され、プロビジョンされた日付)

**メモ:** NetScaler のプライベート IP アドレスはポータルにリストされますが、NetScaler のパブリック IP アドレスはリストされません。 これは、NetScaler の管理はプライベート IP アドレスを使用して行われるのに対し、NetScaler デバイスのパブリック IP アドレスはデバイスの VIP (仮想 IP) として使用され、ロード・バランシング・サービスに用いられるからです。

## 「デバイスの詳細 (Device Details)」画面 

NetScaler の名前をクリックすると、NetScaler の **「デバイスの詳細 (Device Details)」**ページに移動します。このページには、NetScaler がデプロイされた VLAN と、NetScaler のパブリック IP アドレスが表示されます。 これらの IP アドレスは NetScaler のデフォルトのパブリック VIP アドレスであるため、管理には使用できません。 後でこのアドレスを使用して、ロード・バランシングのサービスに関連付けます。

## NetScaler への接続

{{site.data.keyword.BluSoftlayer_notm}} は、フル・ルート・アクセス権限を NetScaler デバイスに付与します。 NetScaler の管理 UI にログインするには、{{site.data.keyword.BluSoftlayer_notm}} プライベート・ネットワークに接続する必要があります ({{site.data.keyword.BluSoftlayer_notm}} 管理 VPN であるか、または {{site.data.keyword.BluSoftlayer_notm}} 環境内のサーバー上のリモート・セッションから管理機能を実行)。 

カスタマー・ポータルから NetScaler の管理 UI に接続するには、**「デバイスの詳細 (Device Details)」** 画面の右上隅にある**「アクション (Actions)」** ドロップダウン・リストをクリックし、**「デバイスの管理 (Manage Device)」** を選択して、ブラウザーで新しいタブまたはポップアップ・ウィンドウを起動します。 これによって、NetScaler の NSIP (前に表示されたプライベート IP アドレス) に転送されます。 表示されるページで、デバイスのルート・ユーザー名とパスワードの入力を求められます。 この情報を入力すると、NetScaler 管理 GUI に移動します。 

あるいは、NetScaler デバイスのプライベート IP をコピーして Web ブラウザーに貼り付けることもできます。

### NetScaler SSH アクセス

任意の SSH クライアントを使用して、NetScaler デバイスに直接接続することもできます。 「デバイス・リスト (Device List)」ページで NetScaler デバイスのプライベート IP とログイン情報を使用して、{{site.data.keyword.BluSoftlayer_notm}} VPN に接続されていることを確認します。 
