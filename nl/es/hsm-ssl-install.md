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

# Instalar el certificado SSL
{: #install-your-ssl-certificate}

En este tema instalará el certificado SSL que ha creado en la guía [paso a paso](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) anterior. Para ello, lleve a cabo el siguiente procedimiento:

1.	Confirme que el certificado está presente en el directorio `/nsconfig/ssl` en Citrix Netscaler VPX.

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	Aunque la clave de certificado esté ubicada en el directorio correcto, debe reconocerse como objeto Citrix Netscaler VPX válido para poder conectarse e interactuar con otros componentes de VPX. Para ello, realice lo siguiente:

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	El mandato anterior utiliza la sintaxis siguiente:

	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	Donde `keyName` es el nombre de la clave creada en IBM© Hardware Security Module (HSM) con el programa de utilidad de CMU. El parámetro `serialNum` es el número de serie de la partición en cuestión. El parámetro `password`, como antes, es la contraseña de la partición en la que están presentes las claves.

	**NOTA:** El mensaje `Internal error` es debido al incremento de tiempo necesario para completar el paso. La clave debería añadirse correctamente. Sin embargo, será necesario tratar cualquier otro mensaje de error que reciba.

3.	Confirme que la clave se ha añadido:

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	De la misma forma que con la clave HSM, el certificado SSL debe añadirse utilizando el mandato de Citrix VPX adecuado para que se reconozca:

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	Para el mandato anterior se utiliza la sintaxis siguiente:

	```
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	Donde `certkey` es el nombre del objeto de certificado que se debe añadir en el dispositivo VPX. El parámetro `cert` contiene el nombre y la vía de acceso al archivo, si está ubicado en un directorio que no sea el actual). Por último, `hsmkey` contiene el nombre de la clave añadida en el paso anterior.

5.	Confirme que el certificado se ha instalado:

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

6.	(OPCIONAL) Para evitar advertencias de seguridad al acceder al contenido mediante un navegador web, es posible que desee instalar certificados "CA intermedios". Estos permiten que Citrix Netscaler VPX comparta información con clientes de conexión.

	Para obtener certificados intermedios para RapidSSL, visite cualquiera de los enlaces siguientes:

	* [Volver a emitir el certificado GeoTrust para pedidos de socios o QuickSSL ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [Certificados CA raíz y RapidSSL intermedio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	Para instalar y enlazar los certificados, siga las instrucciones de este [artículo de Citrix ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://support.citrix.com/article/CTX114146){:new_window}.

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```
