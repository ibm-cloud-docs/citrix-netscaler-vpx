---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, keys, csr

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

# 鍵の作成および証明書署名要求 (CSR) の生成
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

このサブセクションでは、証明書署名要求 (CSR) の生成に使用される鍵ペアを作成し、それを使用して証明書を注文または要求します。

1.	まず、VPX 内のオブジェクト・リストを確認します。 作成中は、このパーティションの指定パスワードを使用します。

	```
	root@IBMADC690867-s6dr# cmu list
	スロット 0 にトークンのパスワードを入力してください: 	**********
	```

	出力が空白または空であるため、オブジェクトが存在しないことが確認できます。

	次に、パーティションの詳細を表示して、HSM でオブジェクトの数が 0 になっていることを確認します。

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	パーティション名:                  partition6
	パーティション SN:                         534071053
	パーティションのラベル:                    partition6
	パーティション所有者のロックアウト:        no
	パーティション所有者の変更対象 PIN:        no
	パーティション所有者のログイン残り試行回数: パーティション所有者がロックアウトされるまで残り 10 回
	レガシー・ドメイン設定済み:                no
	パーティションのストレージ情報 (バイト):   合計 =207559, 使用済み =0, 空き =207559
	パーティションのオブジェクト数:            0

	コマンド結果 : 0 (成功)
	```

	上記にリストされたコマンドは、以下の構文を使用しています。

	```
	partition show -p <partition_name>
	```

2.	VPX で証明書管理ユーティリティー (CMU) を使用して、以下のコマンドにより鍵ペアを作成します。 再度、指定されたパーティション・パスワードを使用します。

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	スロット 0 にトークンのパスワードを入力してください: **********

	RSA メカニズム・タイプを選択してください -
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	上記の構文で、`modulusBits` パラメーターは RSA 鍵の長さ (ビット) を示し、`publicExponent` はそれらの鍵の生成に使用される公開鍵指数の値を定義します。これは 3、17、または 65537 に設定する必要があります。 「label」キーワードを使用して、後で参照したり特定したりしやすいように、タグを指定します。 他の 2 つのパラメーターまたは追加パラメーターについて詳しくは、[「ユーティリティー・リファレンス・ガイド (Utilities Reference Guide)」![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}を参照してください。

3.	オブジェクトが作成されたことを確認します。 VPX では、次のようになります。

	```
	root@IBMADC690867-s6dr# cmu list
	スロット 0 にトークンのパスワードを入力してください: **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	HSM では、次のようになります。

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	パーティション名:                       partition6
	パーティション SN:                              534071053
	パーティションのラベル:                         partition6
	パーティション所有者のロックアウト:             no
	パーティション所有者の変更対象 PIN:         　　no
	パーティション所有者のログイン残り試行回数:     パーティション所有者がロックアウトされるまで残り 10 回
	レガシー・ドメイン設定済み:                　　 no
	パーティションのストレージ情報 (バイト):       合計 =207559, 使用済み =1660,  空き =205899
	パーティションのオブジェクト数:                 2

	コマンド結果 : 0 (成功)
	```

4.	前のステップで作成した鍵を使用して、CMU ユーティリティーで CSR を生成します。

	共通名 (CN) と E メール (E) には、正しい値または適切な値を使用するようにしてください。共通名 (CN) は、仮想サーバー/IP (VPX) と関連付けられた DNS A レコードで使用される FQDN と一致する必要があります。 E パラメーターは、これが要求/注文された後で証明書調達の詳細を送信する際に使用されます。

	```
	root@IBMADC690867-s6dr# cmu requestcertificate

	スロット 0 にトークンのパスワードを入力してください : **********

	サブジェクトの 2 文字の国別コード (C) を入力してください : US
	サブジェクトの州名 (S) を入力してください : North Carolina
	サブジェクトの市区町村 (L) を入力してください : Durham
	サブジェクトの組織名 (O) を入力してください : IBM
	サブジェクトの組織単位名 (OU) を入力してください : HSM
	サブジェクトの共通名 (CN) を入力してください : hsmclient7.projectgoldfinch.net   
	E メール・アドレス (E) を入力してください : user@yourdomain.com
	出力ファイル名を入力してください : certreqnss6dr.csr
	```

	上記にリストされた出力で、ファイル名には拡張子 .csr を持つ任意の名前を指定できますが、分かりやすい説明となる名前を推奨します。

5.	ファイルの作成を確認します。

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
