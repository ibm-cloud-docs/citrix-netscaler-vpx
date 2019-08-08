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

# ポリシー・ベース・ルーティング (PBR) の作成
{: #creating-policy-based-routing}

VPN 接続で使用する固有のトラフィック・パラメーター (ローカル・サブネットとリモート・サブネットなど) を指定するには、ポリシー・ベース・ルーティング (PBR) ポリシーが必要です。PBR プロファイルを作成するには、以下の手順を実行します。

1.	**「System」>「Network」>「PBR」**とナビゲートし、**「Add」**を選択します。
2.	**「Name」**を入力します。
3.	**「Action」**は、デフォルトの設定**「ALLOW」**のままにします。
4.	**「Next Hop Type」**で**「IP Tunnel」**を選択し、[前に作成した](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel)トンネルを**「IP Tunnel Name」**ドロップダウン・リストから選択します。
5.	**「Enable PBR」**にチェック・マークを付けたことを確認します。
6.	**「Configure IP」**セクションで、ソースと宛先の両方の**「Operation」**フィールドに **=** を指定します。
7.	次のフィールドに最初と最後のサブネット IP を指定します。
  *	**Source IP Low**
  *	**Source IP High**
  *	**Destination IP Low**
  *	**Destination IP High**
8.	**「Create」**をクリックします。

    <img src="images/ipseCreatePBR1.png" alt="図" style="width: 200px;"/>

9.	**「System」>「Network」>「PBR」**から新規 PBR を選択し、**「Select Action」**リストをクリックして、**「Apply」**を選択します。

    <img src="images/ipsecCreatePBR2.png" alt="図" style="width: 600px;"/>

CLI で PBR プロファイルを作成するには、次の構文を使用します。

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs
  
  ```
  {: codeblock}

  VPN トンネルを通って VPX の背後に配置する仮想サーバー・インスタンスまたはインフラストラクチャーは、デフォルト・ゲートウェイとして VPX を使用するか、または静的ルートを使用するように構成する必要があることに注意してください。そうすることで、宛先がリモート (ピア) サブネットの場合にトラフィックが VPX に送信されます。以下の静的ルート (**10.115.0.0/16**) の例を確認してください。
  {: note}

  ```
  >route print
  ===========================================================================
  インターフェイス一覧
  3...06 93 7a 03 f0 b3 ......XenServer PV Network Device #0
  4...06 ff 8f 6d 89 e8 ......XenServer PV Network Device #1
  1...........................Software Loopback Interface 1
  7...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
  10...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
  ===========================================================================
  
  IPv4 ルート テーブル
  ===========================================================================
  アクティブ ルート:
  ネットワーク宛先        ネットマスク          ゲートウェイ       インターフェイス メトリック
          0.0.0.0          0.0.0.0    169.54.255.65    169.54.255.73     26
       10.115.0.0      255.255.0.0      192.168.0.1      192.168.0.2     26

  ```
  {: codeblock}
