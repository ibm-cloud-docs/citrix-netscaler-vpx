---

copyright:
  years: 2018, 2019
lastupdated: "2019-11-12"

keywords:

subcollection: citrix-netscaler-vpx


---

{{site.data.keyword.attribute-definition-list}}

# Install your SSL certificate
{: #install-your-ssl-certificate}

You can install the SSL Certificate you created in the previous step-by-step, [Deploying and Configuring the IBM© Hardware Security Module (HSM) with {{site.data.keyword.vpx_full}}](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) for your {{site.data.keyword.vpx_full}}.
{: shortdesc}

To do so, perform the following procedure:

1.	Confirm that the certificate is present in the `/nsconfig/ssl` directory on your {{site.data.keyword.vpx_full}}.

	```sh
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	Even though the certificate key is located in the proper directory, it must be recognized as a valid {{site.data.keyword.vpx_full}} object for it to connect and interact with other VPX components. To do so:

	```sh
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	The previous command uses the following syntax:

	```sh
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	Where `keyName` is the name of the key created on the IBM© Hardware Security Module (HSM) with the CMU utility. The `serialNum` parameter is the serial number of the partition in question. The `password` parameter, as before, is the password of the partition on which the keys are present.

	The `Internal error` message is expected due to the increased time it takes to complete this step. The key should be properly added. However, any other error messages you receive should be addressed.
    {: note}

3.	Confirm the key was added:

	```sh
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	As with the HSM key, the SSL certificate must be added using the appropriate Citrix VPX command for it to be recognized:

	```sh
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	For the previous command the following syntax is used:

	```sh
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	Where `certkey` is the name of the certificate object to be added in the VPX device. The `cert` parameter contains the name and path to the file, if it is located in a directory other than the current one. Lastly, `hsmkey` contains the name of the key added in the previous step.

5.	Confirm the certificate was installed:

	```sh
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