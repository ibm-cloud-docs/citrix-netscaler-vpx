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

# Solicitar um Certificado SSL
{: #order-an-ssl-certificate}

Secure Sockets Layer (SSL) é uma tecnologia que criptografa o tráfego entre o aplicativo cliente e o aplicativo do servidor, e é realizada usando um sistema de chave pública/chave privada que usa um certificado SSL.

Os certificados SSL contêm a chave pública do servidor, as datas para as quais o certificado é válido, um nome do host para o qual o certificado é válido e uma assinatura da autoridade de certificação que os emitiu.

O IBM© Cloud oferece certificados que podem ser adquiridos e comprados sem precisar passar por um fornecedor/site de terceiros.

O IBM Cloud oferece aos clientes certificados SSL anuais e bianuais que oferecem vários benefícios, incluindo:

* Autenticação integral para verificação de identidade de negócios e propriedade de domínio
* Criptografia de 40 a 256 bits em todas as transações on-line
* Varredura diária de malware do website para garantir que seu site e seus clientes estejam protegidos

Se você estiver executando múltiplos domínios, um certificado SSL poderá ser comprado para cada domínio.

Para obter mais informações sobre certificados SSL, consulte os artigos do IBM Cloud a seguir:

* [Sobre certificados SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [Introdução à tecnologia de SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [Planejamento para SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)


Para pedir um certificado SSL para uso com o seu Citrix Netscaler VPX, execute o procedimento a seguir:

1.	Na CLI do shell VPX, exiba o texto CSR abrindo o arquivo CSR anteriormente criado na etapa [Criar chaves e gerar o Certificate Signing Request (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-):

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

2.	Copie o conteúdo do arquivo, começando com `---BEGIN NEW CERTIFICATE REQUEST---` até `---END NEW CERTIFICATE REQUEST---`.

3.	Siga [estas instruções](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates) para fazer o pedido, colando o texto do arquivo CSR no campo apropriado. No exemplo a seguir, `RapidSSL 1 Year` foi escolhido.

	<img src="images/5-Order-Certificate_1.png" alt="drawing" style="width: 550px;"/>

	Conforme mostrado, o sistema processa e interpreta o texto CSR e, em seguida, exibe isso na página a seguir.

	Certifique-se de selecionar uma conta de e-mail válida e um domínio/subdomínio, pois esse é o método designado para validar a propriedade do domínio.

	Confirme os detalhes do pedido e clique em **Fazer pedido**.

4. Você receberá uma confirmação de pedido com os detalhes da solicitação de certificado na conta indicada.

	Clique no link incluído no e-mail para aprovar a solicitação de validação de domínio. Neste momento, a solicitação SSL deve estar pronta para que o cumprimento seja iniciado.
