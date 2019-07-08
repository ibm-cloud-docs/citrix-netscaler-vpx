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

# Installation de votre certificat SSL
{: #install-your-ssl-certificate}

Dans cette rubrique, vous allez installer le certificat SSL créé à la rubrique [pas à pas](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) précédente. Pour ce faire :

1.	Vérifiez que le certificat existe dans le répertoire `/nsconfig/ssl` sur Citrix NetScaler VPX.

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	Même si la clé de certificat se trouve dans le répertoire approprié, elle doit être reconnue en tant qu'objet Citrix NetScaler VPX valide pour pouvoir se connecter et interagir avec d'autres composants VPX. Pour ce faire, procédez comme suit :

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	La commande ci-dessus utilise la syntaxe suivante :

	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	Où `keyName` est le nom de la clé créée sur le module IBM© HSM (Hardware Security Module) à l'aide de l'utilitaire CMU. Le paramètre `serialNum` désigne le numéro de série de la partition concernée et le paramètre `password` est le mot de passe de la partition sur laquelle sont installées les clés.

	Le message `Internal error` est lié à l'augmentation du délai requis pour terminer cette étape. La clé doit être correctement ajoutée. Toutefois, tous les autres messages que vous recevez doivent être traités.
  {: note}

3.	Vérifiez que la clé a été ajoutée :

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	A l'instar de la clé HSM, le certificat SSL doit être ajouté en utilisant la commande Citrix VPX appropriée pour qu'il soit reconnu :

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	La commande ci-dessus a la syntaxe suivante :

	```
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	Où `certkey` est le nom de l'objet de certificat à ajouter au dispositif VPX. Le paramètre `cert` contient le nom et le chemin du fichier, si ce dernier se trouve dans un répertoire autre que celui en cours. Enfin, `hsmkey` indique le nom de la clé ajoutée à l'étape précédente.

5.	Vérifiez que le certificat a été installé :

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

6.	(Facultatif) Pour éviter les avertissements de sécurité lors de l'accès au contenu via un navigateur Web, vous pouvez installer des certificats de type "Autorité de certification intermédiaire". Ceux-ci permettent à Citrix NetScaler VPX de partager ses informations avec les clients qui se connectent.

	Pour obtenir ces certificats intermédiaires pour RapidSSL, cliquez sur l'un des liens suivants :

	* [Reissue GeoTrust Certificate For Partner Orders or QuickSSL ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [RapidSSL Intermediate and Root CA Certificates ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	Pour installer et lier les certificats, suivez les instructions fournies dans cet [article Citrix ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://support.citrix.com/article/CTX114146){:new_window}.

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```
