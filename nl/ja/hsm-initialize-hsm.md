---

copyright:
  years: 2018
lastupdated: "2018-11-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# IBM Hardware Security Module (HSM) の初期化
{: #initialize-ibm-hardware-security-module-hsm-}

ほとんどの構成で HSM デバイスの初期化が必要となります。 これを行わないと、特定の `show` コマンド以外は実行できません。

デバイスを初期化するには、以下のステップに従ってください。

1.	SSH を使用して、**「デバイス」 > 「デバイス・リスト」 > 「HSM 名の展開 (Expand HSM name)」**の下のコントロール・ポータルにリストされている資格情報で IBM© Hardware Security Module デバイスに接続します。

	もしくは、公開鍵認証を使用することもできます。 詳しくは、[アプライアンス管理ガイド (Appliance Administration Guide) (38 ページ) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}を参照してください。

	**注:** SSH アクセスは通常、デフォルトで有効に設定され、許可されています。 SSH での接続に問題がある場合は、ご使用のインフラストラクチャーのルーティングとセキュリティーを確認してください。

2. `hsm init` コマンドを実行します。

	```
	[jpmongehsm2] lunash:>hsm init -l jpmonge

	HSM 管理者のパスワードを入力してください。
	> ********

	確認のためパスワードを再入力してください。
	> ********

	この HSM の初期化に使用する複製ドメインを入力してください。
	> ********

	確認のため複製ドメインを再入力してください。
	> ********

	注意: この HSM を初期化しますか?

	HSM を初期化するには「proceed」を、ここで終了するには「quit」を入力してください。
		> proceed
		「hsm init」が正常に行われました。

	コマンド結果 : 0 (成功)
  	```

	使用された構文は次のようになります。`hsm init -l <hsmlabel>`

`-l` パラメーターまたはラベルは、HSM に ID を割り当てる際に使用したパラメーターです。これには、業務、管理者、またはその管理者が果たす役割に関する意味のあるテキストまたは説明を指定できます。 HSM 管理者パスワードは HSM セキュリティー担当者 (SO) の指定パスワードになり、基本的には暗号オブジェクトの作成と構成、および HSM 環境の変更に必要とされるプロファイルです。

最後に、複製ドメインは、HSM のグループでのオブジェクトの形成を可能にする共有 ID です。 これは通常、バックアップや HA に使用されます。

HSM CLI でサポートされるすべての使用可能コマンドについては、[LunaSH コマンド・リファレンス・ガイド (LunaSH Command Reference Guide) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window}を参照してください。
