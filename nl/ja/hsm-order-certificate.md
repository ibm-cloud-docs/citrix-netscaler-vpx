---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, certificate, order

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

# SSL 証明書の注文
{: #order-an-ssl-certificate}

Secure Sockets Layer (SSL) は、クライアント・アプリケーションとサーバー・アプリケーションの間のトラフィックを暗号化するテクノロジーであり、SSL 証明書を使用した公開鍵/秘密鍵システムを使用することで達成されます。

SSL 証明書には、サーバーの公開鍵、証明書が有効な期間、証明書が有効なホスト名、および証明書を発行した認証局からの署名が入っています。

IBM© Cloud では、サード・パーティー・ベンダーまたはサイトを通さずに取得および購入できる証明書を提供しています。

IBM Cloud では、お客様向けに 1 年ごとおよび 2 年ごとの SSL 証明書を用意し、以下のようなさまざまな利点を提供しています。

* ビジネス ID およびドメイン所有権の検証のための完全認証
* すべてのオンライン・トランザクションに対する 40 ビットから 256 ビットの暗号化
* 毎日 Web サイトのマルウェアをスキャンし、サイトと顧客の両方を確実に保護

複数のドメインを稼働している場合は、ドメインごとに SSL 証明書を購入できます。

SSL 証明書の詳細情報については、IBM Cloud の以下の記事を参照してください。

* [SSL 証明書について](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [SSL テクノロジーの概要](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [SSL の計画](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)

{{site.data.keyword.vpx_full}} で使用する SSL 証明書を注文するには、以下の手順を実行します。

1.	VPX シェル CLI で、[キーの作成と証明書署名要求 (CSR) の生成](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) のステップで以前に作成した CSR ファイルを開いて、CSR テキストを表示します。

	```
	root@IBMADC690867-s6dr# cat certreqnss6dr.csr
	-----BEGIN NEW CERTIFICATE REQUEST-----
	MIIC5jCCAc4CAQAwgaAxCzAJBgNVBAYTMRcwFQYDVQQIEw5Ob3J0aCBDYXJv
	bGluYTEPMA0GA1UEBxMGRHVyaGFtMQwwCgYDVQQKEwNJQk0xDDAKBgNVBAsTA0hT
	TTEoMCYGA1UEAxMfaHNW50Ny5wcm9qZWN0Z29sZGZpbmNoLm5ldDEhMB8G
	CSqGSIb3DQEJARYSanBtb25nZUBjci5pYm0uY29tMIIBIjANBgkqhkiG9w0BAQEF
	/pXQN+a55HhWmnyj5gThAprOoN8DeiVN+1HI+PA+g1
	r4+8dKA1xz+jPhWDQgQYb3Wnh8VK8Ouids6uFnsoc3KDymbzoWZYctp8PA6uBzJ/
	25RGiZquRu9MYJIWkQ46WQ14PoJ8BiYuJa/N6L47+Jr2vaCntmXBU4rFrjctHqq8
	Hct9q5OVYXbYLQB+MM3gYyyFBQpZ1sHZD4D6K3AISRGsOE9rrovGjUfO8mLKE6a
	AQEFBQADggEBAMe+kmdPNtt8LOpaAy+u5i9GpgHfH5zW2sX4Lj7srkqwmyxavqjE
	XvM9PPudXV9OCUWewtlm/Eqo1pYIRudFBrjg5UJyKpM4sWWdKIrTk8RZusdOUvKU
	0vBRJRJ3Yy/1olXFO05FFSotAyB9P5v9siMwdWUhM9pSiGwoNXCB74m2sxgUh10J
	H0IvDl3SL4ptosV10KJtbOiO/YV9XXNaW8/X/2uM9Y3stcnSvzJGrFlPmbhK7Vsd
	uL6/wSnV1E70CDT+KPPapzVJr/S8nP5xHVVl/5/JUGZa8rx01g9EBmX36H3T
	kHD85XOkSI4y04Y3t6pMVbIAz0vipOmHYlM=
	-----END NEW CERTIFICATE REQUEST-----
	```

2.	`---BEGIN NEW CERTIFICATE REQUEST---` から `---END NEW CERTIFICATE REQUEST---` まで、ファイルのコンテンツをコピーします。

3.	[指示](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates)に従って注文を作成し、 CSR ファイル・テキストを適切なフィールドに貼り付けます。 以下の例では、`RapidSSL 1 Year` が選択されています。

	<img src="images/5-Order-Certificate_1.png" alt="図面" style="width: 550px;"/>

	表示されているように、システムは CSR テキストを処理および解釈し、次のページでそれを表示します。

	ドメインの所有権を有効にする指定の方法となるので、必ず有効な E メール・アカウントおよびドメイン / サブドメインを選択してください。

	注文の詳細を確認してから、**「注文の実行 (Place Order)」**をクリックします。

4. 指定したアカウントで、証明書要求の詳細を記載した注文確認を受信します。

	E メールに含まれているリンクをクリックして、ドメイン有効化要求を承認します。 この時点で、SSL 要求のフルフィルメントを開始する準備ができているはずです。
