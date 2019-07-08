---

copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: dns, cache, virtual server

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

# DNS 仮想サーバーの構成
{: #configure-the-dns-virtual-server}

DNS 仮想サーバーを構成するには、以下のようにします。

1. 「トラフィック管理 (Traffic Management)」 > 「ロード・バランシング (Load Balancing)」 > 「サーバー」と移動します。
2. 「追加」をクリックして 2 つの IBM© Softlayer DNS リゾルバー、10.0.80.11 と 10.0.80.12 を追加します。

	<img src="images/fp5.png" alt="図面" style="width: 200px;"/> <img src="images/fp5b.png" alt="図面" style="width: 200px;"/>

3. 次に、「トラフィック管理 (Traffic Management)」> 「ロード・バランシング (Load Balancing)」 > 「サービス・グループ」と移動し、「追加」を選択して、DNS サービス・グループを作成して定義します。

	<img src="images/fp6.png" alt="図面" style="width: 400px;"/>

4. DNS プロトコルを選択して、「OK」をクリックします。

	<img src="images/fp7.png" alt="図面" style="width: 300px;"/>

5. 次の画面で、新規 DNS リゾルバーをメンバー・サーバーとしてこの DNS サービス・グループに追加します。これを行うには、まず**「サービス・グループ・メンバー (Service Group Members)」**の下の空フィールドをクリックします。

6. 「サービス・グループ・メンバーの作成 (Create Service Group Member)」パネルで、DNS ポート 53 を指定して「作成」をクリックします。

	<img src="images/fp8.png" alt="図面" style="width: 200px;"/>

7. 「閉じる」をクリックし、「完了」をクリックします。

	ご使用の Citrix NetScaler VPX アプライアンスから 2 つの IBM Softlayer DNS リゾルバーに到達可能であると想定し、サービス・グループは緑色で表示されます。

8. 次に、「トラフィック管理 (Traffic Management)」 > 「ロード・バランシング (Load Balancing)」 > 「Virtual Server」と移動し、「追加」をクリックして DNS 仮想サーバーを定義します。
9. 「基本設定 (Basic Settings)」の下で仮想サーバーに名前を付け、DNS プロトコルとポート 53 を選択して、ご使用のプライベート・サブネットから IP アドレスを割り当てます。

	<img src="images/fp9.png" alt="図面" style="width: 300px;"/>

10. 次のページで、**「ロード・バランシング仮想サーバーのサービス・グループ・バインディングがない (No Load Balancing virtual Server ServiceGroup Binding)」** というラベルが付いた空フィールドをクリックします。
11. 前に定義した DNS サービス・グループをドロップダウン・リストから選択し、「バインド (Bind)」をクリックします。  

	<img src="images/fp10.png" alt="図面" style="width: 300px;"/>

12. 「続行」をクリックし、次に「完了」をクリックします。

DNS 仮想サーバーの状態が緑色で表示されるようになりました。

<img src="images/fp11.png" alt="図面" style="width: 500px;"/>
