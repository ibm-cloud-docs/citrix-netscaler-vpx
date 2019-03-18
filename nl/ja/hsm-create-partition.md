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

# パーティションの作成
{: #create-a-partition}

パーティションとは、HSM エンジン内で暗号オブジェクトを要求または作成するクライアントに関連付けまたは接続された論理スペースまたは独立スペースです。 各パーティションは、他のパーティションとは分離された独自のデータおよびポリシーを持っています。 パーティションについて詳しくは、[管理ガイド (Administration Guide) (211 ページ) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}を参照してください。

パーティションを作成するには、以下の手順を実行します。

1.	[初期化](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-)中に指定したパスワードを使用して、以下のように HSM セキュリティー担当者または管理者としてログインします。

	```
	[jpmongehsm2] lunash:>hsm login

	HSM 管理者のパスワードを入力してください。
	> ********

	「hsm login」が正常に行われました。

	コマンド結果 : 0 (成功)
	```

2.	HSM 管理者ログイン状況が「ログイン済み (Logged In)」になっていることを確認します。

	```
	[jpmongehsm2] lunash:>hsm show

	アプライアンスの詳細:
	==================
	ソフトウェアのバージョン:                6.2.2-5

	HSM の詳細:
	============
	HSM ラベル:                         jpmonge
	シリアル #:                         534071
	ファームウェア:                     6.10.9
	HSM モデル:                         K6 Base
	認証方式:             　　　　　　　パスワード
	HSM 管理者ログイン状況:             ログイン済み
	HSM 管理者ログイン残り試行回数:     HSM ゼロ化まで残り 3 回
	RPV 初期化済み:                     No
	監査役割初期化済み:             　　No
	リモート・ログイン初期化済み:     　No
	手動ゼロ化済み:             　　　  No
	[出力省略]
	```

	上記出力で、HSM 管理者ログイン状況には`ログイン済み`と表示されていなければなりません。 そうでない場合、次のセクションにリストするほとんどの操作およびコマンドは、管理者権限が必要であるため、失敗します。

3.	既存パーティションのリスト:

	```
	[jpmongehsm2] lunash:>partition list
	ストレージ (バイト)
	----------------------------
	パーティション       名前             オブジェクト   	合計  使用済み  空き
	===================================
	534071016            partition1                   0  207559       0  207559 	534071020            partition2                   3  207559    3464  204095
	534071027            partition3                   0  207559       0  207559
	534071021            partition4                   2  207559    1652  205907
	534071030            partition5                  10  207559    9400  198159

	コマンド結果 : 0 (成功)
	```

	この出力には 5 つの既存パーティションが表示されています。

4.	パーティションの新規作成:

	**注:** このステップで定義されるパスワードは、後で Citrix VPX HSM クライアント・プロセスでオブジェクトを関連付けおよび作成する際に使用します。 後で参照できるよう、このパスワードを記録しておいてください。 また、初期化プロセス中に定義した複製ドメインを使用するようにしてください。

	```
	[jpmongehsm2] lunash:>partition create -partition partition6

	完了後のパーティション数は次のようになります: 6

	-label:  Not provided; using name for label.

	パーティションのパスワードを入力してください。
	> **********

	確認のためパスワードを再入力してください。
	> **********

	このパーティションの作成時に使用する複製ドメインを入力してください。
	> ********

	確認のため複製ドメインを再入力してください。
	> ********

	初期化済みのパーティションを作成するには「proceed」を、ここで終了するには「quit」を入力してください。
		> proceed
	「partition create」が正常に行われました。

	コマンド結果 : 0 (成功)
	```

	構文は次のようになります。

	```
	partition create -partition <name-for-new-Partition>
	```

5.	新規パーティションが作成されたことを確認します。

	```
	[jpmongehsm2] lunash:>partition list

	ストレージ (バイト)	                                             	----------------------------
	パーティション        名前             オブジェクト   合計  使用済み  空き
	===========================================
	534071016            partition1                   0  207559       0  207559
	534071020            partition2                   3  207559    3464  204095
	534071027            partition3                   0  207559       0  207559
	534071021            partition4                   2  207559    1652  205907
	534071030            partition5                  10  207559    9400  198159
	534071053            partition6                   0  207559       0  207559

	コマンド結果 : 0 (成功)
	```

	`Partition List` コマンドの出力に、6 つのパーティションが表示されるようになりました。
