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

# Instalar seu Certificado SSL
{: #install-your-ssl-certificate}

Neste tópico, você instalará o Certificado SSL que criado na [Etapa por etapa](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) anterior. Para
fazer isso, execute o procedimento a seguir:

1.	Confirme se o certificado está presente no diretório `/nsconfig/ssl` em seu {{site.data.keyword.vpx_full}}.

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	Embora a chave do certificado esteja localizada no diretório adequado, ela deve ser reconhecida como um objeto válido do {{site.data.keyword.vpx_full}} para que possa se conectar e interagir com outros componentes do VPX. Para isso:

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	O comando anterior usa a sintaxe a seguir:

	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	Em que `keyName` é o nome da chave criada no IBM© Hardware Security Module (HSM) com o utilitário CMU. O parâmetro `serialNum` é o número de série da partição em questão. O parâmetro `password`, como antes, é a senha da partição na qual as chaves estão presentes.

	A mensagem `Internal error` é esperada devido ao maior tempo necessário para concluir essa etapa. A chave deve ser incluída corretamente. No entanto, quaisquer outras mensagens de erro que você receber devem ser endereçadas.
  {: note}

3.	Confirme se a chave foi incluída:

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	Assim como com a chave HSM, o certificado SSL deve ser incluído usando o comando apropriado do Citrix VPX para que ele seja reconhecido:

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	Para o comando acima, a sintaxe a seguir é usada:

	```
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	Em que `certkey` é o nome do objeto de certificado a ser incluído no dispositivo VPX. O parâmetro `cert` contém o nome e o caminho para o arquivo, se ele estiver localizado em um diretório diferente do atual). Por último, `hsmkey` contém o nome da chave incluída na etapa anterior.

5.	Confirme se o certificado foi instalado:

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

6.	(OPCIONAL) Para evitar avisos de segurança ao acessar o conteúdo por meio de um navegador da web, talvez você queira instalar certificados "CA Intermediário". Eles permitem que o {{site.data.keyword.vpx_full}} compartilhe informações com os clientes em conexão.

	Para obter esses certificados intermediários para RapidSSL, visite qualquer um dos links abaixo:

	* [Reemitir o certificado GeoTrust para pedidos de parceiro ou QuickSSL ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [Certificados de autoridade de certificação raiz intermediários e de raiz RapidSSL ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	Para instalar e vincular os certificados, siga as instruções neste [Artigo do Citrix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.citrix.com/article/CTX114146){:new_window}.

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```
