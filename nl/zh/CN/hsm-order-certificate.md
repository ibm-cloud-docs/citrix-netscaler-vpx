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

# 订购 SSL 证书
{: #order-an-ssl-certificate}

安全套接字层 (SSL) 是一种技术，用于对客户机应用程序与服务器应用程序之间的流量进行加密，加密通过使用 SSL 证书的公用密钥/专用密钥系统来完成。

SSL 证书包含服务器的公用密钥、证书的有效日期、证书有效所针对的主机名以及颁发证书的认证中心的签名。

IBM© Cloud 提供了无需经过第三方供应商/站点即可获取和购买的证书。

IBM Cloud 为客户提供一年和两年 SSL 证书，这些证书提供了多种优点，包括：

* 针对业务身份和域所有权验证进行完整认证
* 对所有联机事务进行 40 到 256 位加密
* 每日 Web 站点恶意软件扫描，以确保站点和客户都受保护

如果正在运行多个域，那么可以为每个域购买一个 SSL 证书。

有关 SSL 证书的更多信息，请参阅以下 IBM Cloud 文章：

* [关于 SSL 证书](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [SSL 技术简介](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [规划 SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)


要订购 SSL 证书以用于 Citrix NetScaler VPX，请执行以下过程：

1.	在 VPX shell CLI 中，通过打开先前在[创建密钥并生成证书签名请求 (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) 步骤中创建的 CSR 文件来显示 CSR 文本：

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

2.	复制该文件从 `---BEGIN NEW CERTIFICATE REQUEST---` 开始一直到 `---END NEW CERTIFICATE REQUEST---` 的所有内容。

3.	遵循[这些指示信息](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates)下单，并在相应的字段中粘贴 CSR 文件文本。在以下示例中，选择了 `RapidSSL 1 Year`。

	<img src="images/5-Order-Certificate_1.png" alt="图样" style="width: 550px;"/>

	如图所示，系统将处理并解释 CSR 文本，然后在下一个页面中显示此文本。

	确保选择有效的电子邮件帐户和域/子域，因为这是验证域所有权的指定方法。

	确认订单详细信息，然后单击**下订单**。

4. 您将收到订单确认信息，其中包含您指示的帐户的证书请求的详细信息。

	单击电子邮件中附带的链接以核准域验证请求。此时，SSL 请求应该已准备就绪，可开始执行。
