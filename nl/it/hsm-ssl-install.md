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

# Installazione del tuo certificato SSL
{: #install-your-ssl-certificate}

In questo argomento, installerai il certificato SSL che hai creato nella fase [passo dopo passo](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) precedente. Per eseguire tale operazione, esegui la seguente procedura:

1.	Conferma che il certificato è presente nella directory `/nsconfig/ssl` sul tuo {{site.data.keyword.vpx_full}}.

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	Anche se la chiave di certificato si trova nella directory corretta, deve essere riconosciuta come un oggetto {{site.data.keyword.vpx_full}} valido affinché possa collegarsi e interagire con gli altri componenti VPX. Per eseguire tale operazione:

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	Il precedente comando utilizza la seguente sintassi:

	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	Dove `keyName` è il nome della chiave creata su IBM© Hardware Security Module (HSM) con il programma di utilità CMU. Il parametro `serialNum` è il numero di serie della partizione in questione. Il parametro `password`, come in precedenza, è la password della partizione in cui sono presenti le chiavi.

	Il messaggio `Internal error` è un messaggio previsto a causa dell'aumento del tempo di completamento di questo passo. La chiave deve essere aggiunta correttamente. Tuttavia, devi risolvere tutti gli altri messaggi di errore che dovessi ricevere.
  {: note}

3.	Conferma che la chiave è stata aggiunta:

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	Analogamente alla chiave HSM, il certificato SSL deve essere aggiunto utilizzando il comando Citrix VPX appropriato affinché possa essere riconosciuto:

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	Per il comando sopra riportato viene utilizzata la seguente sintassi:

	```
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	Dove `certkey` è il nome dell'oggetto certificato da aggiungere nel dispositivo VPX. Il parametro `cert` contiene il nome e il percorso al file, nel caso in cui si trovi in una directory diversa da quella corrente. Infine, `hsmkey` contiene il nome della chiave aggiunta nel passo precedente.

5.	Conferma che il certificato è stato installato:

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

6.	(FACOLTATIVO) Per evitare avvertenze di sicurezza quando accedi al contenuto tramite un browser web, potresti voler installare i certificati "Intermediate CA". Questi certificati consentono al tuo {{site.data.keyword.vpx_full}} di condividere le informazioni con i client collegati.

	Per ottenere questi certificati intermedi per RapidSSL, visita uno dei link riportati di seguito:

	* [Reissue GeoTrust Certificate For Partner Orders or QuickSSL ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [RapidSSL Intermediate and Root CA Certificates ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	Per installare e collegare i certificati, segui le istruzioni presenti in questo [articolo Citrix ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://support.citrix.com/article/CTX114146){:new_window}.

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```
