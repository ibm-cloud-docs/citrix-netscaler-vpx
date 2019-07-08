---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, redirect, ssl, traffic

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

# SSL トラフィック用のキャッシュのリダイレクトの構成 (オプション)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

(前のステップで説明したように) HTTP または HTTPS プロトコルを使用して仮想サーバー用にキャッシュのリダイレクトを定義する代わりに、SSL トラフィックを処理するよう定義することが必要な場合もあります。

これを行うには、以下の手順を実行します。

1. **「トラフィック管理 (Traffic Management)」 > 「キャッシュのリダイレクト」 > 「Virtual Server」**と移動し、**「追加」**をクリックします。 フォワード・プロキシー仮想サーバーの名前を指定し、SSL プロトコルと**「フォワード (FORWARD)」**のキャッシュ・タイプを選択します。 プライベート・サブネットから、必要ポートと共にこれに IP アドレスを割り当てます。

	<img src="images/fp14.png" alt="図面" style="width: 300px;"/>

	**「OK」**をクリックします。

2. 要約ページを確認し、**「OK」**をクリックして先に進みます。
3. リダイレクト、DNS 仮想サーバー、および宛先仮想サーバーの構成を指定します。
4. **「詳細設定」**パネルの下の**「証明書」**をクリックし、SSL 証明書に関する構成を表示します。
5. 空のフィールド**「サーバー証明書がありません (No Server Certificate)」**をクリックします。
6. 「サーバー証明書の選択 (Select Server Certificate)」ドロップダウン・リストから、SSL サーバーを選択します。
7. 必要に応じて証明書の構成情報を入力します。

	<img src="images/fp15.png" alt="図面" style="width: 400px;"/>

	**「インストール」**をクリックします。

8. **「バインド (Bind)」**を選択します。

	<img src="images/fp16.png" alt="図面" style="width: 300px;"/>
