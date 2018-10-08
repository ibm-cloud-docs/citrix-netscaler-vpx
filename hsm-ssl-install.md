---

copyright:
  years: 2018
lastupdated: "2018-09-20"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Install Your SSL Certificate
In this topic you will install the SSL Certificate you created in the previous [Step by Step](hsm-order-certificate.html). To do so, perform the following procedure:

1.	Confirm that the certificate is present in the `/nsconfig/ssl` directory on your Citrix Netscaler VPX.

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	Even though the certificate key is located in the proper directory, it must be recognized as a valid Citrix Netscaler VPX object for it to connect and interact with other VPX components. To do so:

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```
	
	The previous command uses the following syntax:
	
	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```
	
	Where `keyName` is the name of the key created on the IBM Hardware Security Monitor (HSM) with the CMU utility. The `serialNum` parameter is the serial number of the partition in question. The `password` parameter, as before, is the password of the partition on which the keys are present.

	**NOTE:** The `Internal error` message is expected due to the increased time it takes to complete this step. The key should be properly added. However, any other error messages you receive should be addressed.

3.	Confirm the key was added:

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```
	
4.	As with the HSM key, the SSL certificate must be added using the appropriate Citrix VPX command for it to be recognized:

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```
	
	For the above command the following syntax is used:
	
	```
	add ssl certkey <CertkeyName> -cert <cert path/name> 
	-hsmkey <KeyName>
	```
	
	Where `certkey` is the name of the certificate object to be added in the VPX device. The `cert` parameter contains the name and path to the file, if it is located in a directory other than the current one). Lastly, `hsmkey` contains the name of the key added in the previous step.

5.	Confirm the certificate was installed:

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
	
6.	(OPTIONAL) To avoid security warnings when accessing content through a web browser, you may wish to install "Intermediate CA" certificates. These allow your Citrix Netscaler VPX to share information with connecting clients.

	To obtain these intermediate certificates for RapidSSL, visit any of the links below:
	
	* [RapidSSL Intermediate and Root CA Certificates](https://knowledge.digicert.com/generalinformation/INFO1548.html#links)
	* [Reissue GeoTrust Certificate For Partner Orders or QuickSSL](https://knowledge.digicert.com/solution/SO5989.html)

	To install and link the certificates, follow the instructions in this [Citrix article](https://support.citrix.com/article/CTX114146).

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```