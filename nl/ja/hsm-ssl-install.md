---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, install, ssl, certificate, security

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:table: .aria-labeledby="caption"}

# SSL 証明書のインストール
{: #install-your-ssl-certificate}

このトピックでは、以前の [ステップバイステップ](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx)で作成した SSL 証明書をインストールします。 それを行うには、以下の手順を実行します。

1.	Citrix Netscaler VPX 上の `/nsconfig/ssl` ディレクトリーに証明書が存在することを確認します。

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	証明書鍵が適切なディレクトリーに配置されている場合でも、他の VPX コンポーネントと接続し、相互作用するには、有効な Citrix Netscaler VPX オブジェクトとして認識される必要があります。 構成するには、以下の手順に従ってください。

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	上記のコマンドは、以下の構文を使用しています。

	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	ここで、`keyName` は、CMU ユーティリティーを使用して IBM© Hardware Security Module (HSM) 上に作成された鍵の名前です。 `serialNum` パラメーターは、対象となる区画のシリアル番号です。 `password` パラメーターは、以前と同様に、鍵が存在する区画のパスワードです。

	この手順は完了するまでに長い時間がかかるので、`Internal error` メッセージが予期されます。鍵は適切に追加されるはずです。 ただし、これ以外のエラー・メッセージを受け取った場合は、対処が必要になります。
  {: note}

3.	鍵が追加されたことを確認します。

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	HSM 鍵と同様に、SSL 証明書が認識されるようにするには、適切な Citrix VPX コマンドを使用して SSL 証明書を追加する必要があります。

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	上記のコマンドでは、以下の構文を使用しています。

	```
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	ここで、`certkey` は、VPX デバイスに追加する証明書オブジェクトの名前です。 `cert` パラメーターは、(ファイルが現行ディレクトリー以外のディレクトリーに配置されている場合) ファイルの名前とパスを含みます。 最後に、`hsmkey` は、以前のステップで追加された鍵の名前を含みます。

5.	証明書がインストールされたことを確認します。

	```
	> show ssl certKey
	[OUTPUT OMITTED]
		2) Name: hsmclient7ns
		Cert Path: /nsconfig/ssl/hsmclient7.cer
		HSM Key ID: NSkey_s6dr
		Format: PEM
		Status: Valid,   Days to expiration:350
		Certificate Expiry Monitor: ENABLED
		Expiry Notification period: 30 days
		Certificate Type: "Client Certificate" "Server Certificate"
		Version: 3
		Serial Number: 01785B2B61C8D7F1C06AC7CA8EDD573D
		Signature Algorithm: sha256WithRSAEncryption
		Issuer:  C=US,O=DigiCert
	Inc,OU=www.digicert.com,CN=RapidSSL RSA CA 2018
		Validity
			Not Before: Jul 26 00:00:00 2018 GMT
			Not After : Jul 26 12:00:00 2019 GMT
		Subject:  CN=hsmclient7.projectgoldfinch.net
		Public Key Algorithm: rsaEncryption
		Public Key size: 2048
		Ocsp Response Status: NONE
	[OUTPUT OMITTED]
	Done
	>
	```

6.	(オプション) Web ブラウザーを介してコンテンツにアクセスするときにセキュリティー警告を回避するには、「中間 CA」証明書をインストールします。 それらによって、Citrix Netscaler VPX は、接続するクライアントと情報を共有することができます。

	RapidSSL 用にこれらの中間証明書を取得するには、以下のいずれかのリンクにアクセスしてください。

	* [パートナー・オーダーまたは QuickSSL 用の GeoTrust 証明書の再発行 (Reissue GeoTrust Certificate For Partner Orders or QuickSSL)![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [RapidSSL の中間証明書および Root CA 証明書 (RapidSSL Intermediate and Root CA Certificates)![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	証明書をインストールし、リンク付するには、この [Citrix 記事 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://support.citrix.com/article/CTX114146){:new_window} の説明に従ってください。

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```
