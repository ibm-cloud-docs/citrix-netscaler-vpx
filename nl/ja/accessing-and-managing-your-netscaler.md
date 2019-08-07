---
copyright:
  years: 1994, 2019

lastupdated: "2019-06-11"

keywords: manage, managing, locating, details, portal, device, list

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.vpx_full}} の管理
{: #managing-your-citrix-netscaler-vpx}

Citrix NetScaler デバイスは、さまざまな方法で {{site.data.keyword.cloud}} ソリューションを拡張および改良するのに役立つ豊富な機能を備えた強力なツールです。 {{site.data.keyword.cloud_notm}} インフラストラクチャー・カスタマー・ポータルでデバイスの情報を見ることができるほか、デバイスに接続してそのフィーチャーを構成することもできます。  

## カスタマー・ポータルでの NetScaler の詳細の表示
{: #locating-netscaler-details-in-the-customer-portal}

Citrix NetScaler デバイスは、{{site.data.keyword.cloud_notm}} プラットフォーム上にある他のサーバーと同様に、デバイス・リストにリストされます。

デバイス・リストを見つけるには、以下のようにします。

1. ブラウザーから[カスタマー・ポータル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){: new_window} を開き、アカウントにログインします。
2. カスタマー・ポータルのナビゲーションで、**「デバイス (Devices)」>「デバイス・リスト (Device List)」**を選択します。

ご使用のデバイスが、デバイス名でソートされて表示されます。 {{site.data.keyword.vpx_full}} デバイスのデバイス・タイプは「NetScaler」です。

NetScaler の行の左側で、矢印をクリックして行を展開し、NetScaler 管理アクセス用のユーザー名とマスクされたパスワードを表示します。

デバイス・リストにリストされるその他の詳細には、以下のものがあります。

* ロケーション (NetScaler があるデータ・センター)
* プライベート IP アドレス (管理機能を目的として NetScaler に接続するために使用されます)
* 開始日 (マシンが発注され、プロビジョンされた日付)

NetScaler のプライベート IP アドレスはポータルにリストされますが、NetScaler のパブリック IP アドレスはリストされません。NetScaler の管理はプライベート IP アドレスを使用して行うからです。NetScaler デバイスのパブリック IP アドレスは、デバイスの VIP (仮想 IP) として使用され、ロード・バランシング・サービスに使用されます。
{: note}

## 「デバイスの詳細 (Device Details)」画面
{: #the-device-details-screen}

NetScaler の名前をクリックすると、NetScaler の **「デバイスの詳細 (Device Details)」**ページに移動します。このページには、NetScaler がデプロイされた VLAN と、NetScaler のパブリック IP アドレスが表示されます。 これらの IP アドレスは NetScaler のデフォルトのパブリック VIP アドレスであるため、管理には使用できません。 後でこのアドレスを使用して、ロード・バランシングのサービスに関連付けます。

## NetScaler への接続
{: #connecting-to-the-netscaler}

{{site.data.keyword.cloud_notm}} は、フル・ルート・アクセス権限を NetScaler デバイスに付与します。 NetScaler の管理 UI にログインするには、{{site.data.keyword.cloud_notm}} プライベート・ネットワークに接続する必要があります ({{site.data.keyword.BluSoftlayer_notm}} 管理 VPN であるか、または {{site.data.keyword.cloud_notm}} 環境内のサーバー上のリモート・セッションから管理機能を実行)。

カスタマー・ポータルから NetScaler の管理 UI に接続するには、**「デバイスの詳細 (Device Details)」**画面の右上隅にある**「アクション (Actions)」**ドロップダウン・リストをクリックし、**「デバイスの管理 (Manage Device)」**を選択して、ブラウザーで新しいタブまたはポップアップ・ウィンドウを起動します。これによって、NetScaler の NSIP (前に表示されたプライベート IP アドレス) に転送されます。 表示されるページで、デバイスのルート・ユーザー名とパスワードの入力を求められます。 この情報を入力すると、NetScaler 管理 GUI に移動します。

あるいは、NetScaler デバイスのプライベート IP をコピーして Web ブラウザーに貼り付けることもできます。

### NetScaler SSH アクセス
{: #netscaler-ssh-access}

任意の SSH クライアントを使用して、NetScaler デバイスに直接接続することもできます。 「デバイス・リスト (Device List)」ページで NetScaler デバイスのプライベート IP とログイン情報を使用して、{{site.data.keyword.cloud_notm}} VPN に接続されていることを確認します。
