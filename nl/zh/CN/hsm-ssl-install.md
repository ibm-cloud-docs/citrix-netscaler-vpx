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

# 安装 SSL 证书
{: #install-your-ssl-certificate}

在本主题中，将安装您在先前的[逐步指南](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx)中创建的 SSL 证书。为此，请执行以下过程：

1.	确认证书是否位于 {{site.data.keyword.vpx_full}} 上的 `/nsconfig/ssl` 目录中。

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	尽管证书密钥位于正确的目录中，该密钥还必须可识别为有效的 {{site.data.keyword.vpx_full}} 对象，才能与其他 VPX 组件连接并进行交互。为此，请执行以下操作：

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	上面的命令使用以下语法：

	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	其中，`keyName` 是使用 CMU 实用程序在 IBM© Hardware Security Module (HSM) 上创建的密钥的名称。`serialNum` 参数是相关分区的序列号。如前所述，`password` 参数是密钥所在的分区的密码。

	由于完成此步骤需要更长时间，因此预期会显示`内部错误`消息。密钥应该会正确添加。但是，如果收到其他任何错误消息，应进行相应处理。
  {: note}

3.	确认密钥是否已添加：

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	与 HSM 密钥一样，必须使用相应的 Citrix VPX 命令添加 SSL 证书以便识别到该证书：

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	对于以上命令，使用以下语法：

	```
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	其中，`certkey` 是要在 VPX 设备中添加的证书对象的名称。`cert` 参数包含文件的名称和路径（如果文件位于非当前目录中）。最后，`hsmkey` 包含先前步骤中添加的密钥的名称。

5.	确认证书是否已安装：

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

6.	（可选）为了避免通过 Web 浏览器访问内容时出现安全警告，您可能希望安装“中间 CA”证书。这些证书支持 {{site.data.keyword.vpx_full}} 与连接的客户机共享信息。

	要获取 RapidSSL 的中间证书，请访问下列任一链接：

	* [Reissue GeoTrust Certificate For Partner Orders or QuickSSL ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [RapidSSL Intermediate and Root CA Certificates ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	要安装和链接证书，请遵循此 [Citrix 文章 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://support.citrix.com/article/CTX114146){:new_window} 中的指示信息。

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```
