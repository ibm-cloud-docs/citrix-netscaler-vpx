---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, security, create, apply, cipher, suite

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

# 新規の暗号スイートの作成と適用
{: #create-and-apply-a-new-cipher-suite}

暗号スイートは、SSL プロトコルおよび TLS プロトコルのセキュリティー設定をネゴシエーションするために使用される認証、暗号化、メッセージ認証コード (MAC)、および鍵交換アルゴリズムの組み合わせです。

適切な認証を保証するには、Citrix Netscaler VPX で暗号の最適な組み合わせを使用する必要があります。

SSL 暗号スイートおよびその他のベスト・プラクティスの詳細については、以下のリンクにアクセスしてください。

* [Citrix NetScaler を使用して SSLlabs.com で A+ のスコアを獲得 (Scoring an A+ at SSLlabs.com with Citrix Netscaler)![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.citrix.com/blogs/2018/05/16/scoring-an-a-at-ssllabs-com-with-citrix-netscaler-q2-2018-update/){:new_window} – 2018 年 Q2 のアップデート (コマンド・ガイドのステップ 3 および 5 を参照)
* [SSL および TLS のデプロイメントに関するベスト・プラクティス (SSL and TLS Deployment Best Practices)![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices#23-use-secure-cipher-suites){:new_window}
* [NetScaler 上で ECC をセットアップする方法 (How Do I Setup ECC on NetScaler?)![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://support.citrix.com/article/CTX205289){:new_window}

このトピックでは、SSL 暗号の具体的な構成および必要な構成について焦点を当てます。上記のリンクでは、SSL 操作を最適化するために適用できる追加設定に関する情報が記載されています。
{: note}

AEAD、ECDHE、および ECDSA 暗号を優先順位付けする新しい暗号スイートを作成するには、以下の手順を実行します。

1.	Citrix VPX CLI で以下のコマンドを同時に入力し、それらすべてが適用されることを確認します。

	```
	add ssl cipher SSLLABS
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-256-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-256-CBC-SHA
	```

	上記のコマンドの構文は、以下のとおりです。

	```
	add ssl cipher <cipherGroupName>
	bind ssl cipher <cipherGroupName> -cipherName <string>
	```

2.	暗号が Citrix Netscaler VPX に追加されたことを確認します。

	```
	> show ssl cipher SSLLABS
	1)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256       Priority : 1
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02b
	2)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384       Priority : 2
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc02c
	3)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES128-SHA256   Priority : 3
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA-256   HexCode=0xc023
	4)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES256-SHA384   Priority : 4
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA-384   HexCode=0xc024
	5)      Cipher Name: TLS1-ECDHE-ECDSA-AES128-SHA        Priority : 5
	        Description: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA1   HexCode=0xc009
	6)      Cipher Name: TLS1-ECDHE-ECDSA-AES256-SHA        Priority : 6
	        Description: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA1   HexCode=0xc00a
	7)      Cipher Name: TLS1.2-ECDHE-RSA-AES128-GCM-SHA256 Priority : 7
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02f
	8)      Cipher Name: TLS1.2-ECDHE-RSA-AES256-GCM-SHA384 Priority : 8
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc030
	9)      Cipher Name: TLS1.2-ECDHE-RSA-AES-128-SHA256    Priority : 9
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA-256   HexCode=0xc027
	10)     Cipher Name: TLS1.2-ECDHE-RSA-AES-256-SHA384    Priority : 10
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA-384   HexCode=0xc028
	11)     Cipher Name: TLS1-ECDHE-RSA-AES128-SHA  Priority : 11
	        Description: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0xc013
	12)     Cipher Name: TLS1-ECDHE-RSA-AES256-SHA  Priority : 12
	        Description: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0xc014
	13)     Cipher Name: TLS1.2-DHE-RSA-AES128-GCM-SHA256   Priority : 13
	        Description: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0x009e
	14)     Cipher Name: TLS1.2-DHE-RSA-AES256-GCM-SHA384   Priority : 14
	        Description: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0x009f
	15)     Cipher Name: TLS1-DHE-RSA-AES-128-CBC-SHA       Priority : 15
	        Description: SSLv3 Kx=DH       Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x0033
	16)     Cipher Name: TLS1-DHE-RSA-AES-256-CBC-SHA       Priority : 16
	        Description: SSLv3 Kx=DH       Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0039
	17)     Cipher Name: TLS1-AES-128-CBC-SHA       Priority : 17
	        Description: SSLv3 Kx=RSA      Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x002f
	18)     Cipher Name: TLS1-AES-256-CBC-SHA       Priority : 18
	        Description: SSLv3 Kx=RSA      Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0035
 	Done
 	```

3.	仮想サーバーからデフォルトの暗号スイートをアンバインドし、上記のステップで作成したカスタム・グループをバインドします。

	```
	unbind ssl vserver https_vip2 -cipherName DEFAULT

	bind ssl vserver https_vip2 -cipherName SSLLABS

	bind ssl vserver https_vip2 -eccCurveName ALL
	```

	上記のコマンドの構文は次のとおりです。

	```
	unbind ssl cipher <cipherGroupName> -cipherName <string>
	bind ssl vserver <vServerName> -cipherName <string>
	bind ssl vserver <vServerName> -eccCurveName <eccCurveName>
	```

4.	仮想サーバーへの変更を確認します。

	```
	> show ssl vserver https_vip2

	[OUTPUT OMITTED]
		ECC Curve: P_256, P_384, P_224, P_521

	1)      CertKey Name: hsmclient7ns      Server Certificate

	1)      Cipher Name: SSLLABS
		Description: User Created Cipher Group
 	Done
	```

5.	(オプション) ユーザーが (HTTPS 要求ではなく) HTTP 要求を作成した場合に、ユーザーをセキュアな Web サイトにリダイレクトするために、HTTP リダイレクトを使用可能にすることができます。

	構成の説明については、[NetScaler で HTTP から HTTPS へのリダイレクトを構成する方法 (How to Configure HTTP to HTTPS Redirection on NetScaler) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://support.citrix.com/article/CTX201201){:new_window} を参照してください。

6.	Web ブラウザーを開いて FQDN を入力し、HTTPS 接続をテストします。 サイトは、Citrix VPX の背後にある HTTP サービスによってレンダリングされたコンテンツをロードするはずです。

	ブラウザー内の URL の横にあるパッドロック・アイコンをクリックして証明書情報を表示し、証明書の情報を確認することもできます。

	<img src="images/21-check-certificate.png" alt="図面" style="width: 350px;"/>

	ステップ 5 でリダイレクトを構成した場合、HTTP 要求を使用したときもセキュアなサイトがロードされます。
