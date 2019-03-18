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

# SSL-Zertifikat installieren
{: #install-your-ssl-certificate}

In diesem Abschnitt erfahren Sie, wie Sie das SSL-Zertifikat, das Sie in der vorherigen [schrittweisen Anleitung](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) erstellt haben, installieren. Gehen Sie hierfür wie folgt vor:

1.	Vergewissern Sie sich, dass das Zertifikat im Verzeichnis `/nsconfig/ssl` in Ihrer Citrix NetScaler VPX-Instanz vorhanden ist.

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	Auch wenn sich der Zertifikatsschlüssel im richtigen Verzeichnis befindet, muss er als gültiges Citrix NetScaler VPX-Objekt erkannt werden, damit er eine Verbindung zu anderen VPX-Komponenten herstellen und mit diesen interagieren kann. Gehen Sie hierfür wie folgt vor:

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	Die Syntax des vorangegangenen Befehls lautet wie folgt:

	```
	add ssl hsmkey <Schlüsselname> -hsmType SAFENET -serialNum 	<Seriennummer> -password <Kennwort>
	```

	Dabei ist `Schlüsselname` der Name des Schlüssels, der im IBM© Hardware Security Module (HSM) mit dem Dienstprogramm CMU erstellt wurde. Der Parameter `serialNum` gibt die Seriennummer der betreffenden Partition an. Der Parameter `password` gibt wieder das Kennwort der Partition an, in der sich die Schlüssel befinden.

	**HINWEIS:** Die Nachricht wegen eines internen Fehlers (`Internal error`) wird erwartet, weil die Ausführung dieses Schritts sehr viel Zeit in Anspruch nimmt. Der Schlüssel sollte trotzdem ordnungsgemäß hinzugefügt werden. Auf alle anderen Fehlernachrichten, die Sie erhalten, müssen Sie jedoch reagieren.

3.	Überprüfen Sie, ob der Schlüssel hinzugefügt wurde:

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	Wie bei dem HSM-Schlüssel muss das SSL-Zertifikat mit dem entsprechenden Citrix VPX-Befehl hinzugefügt werden, damit es erkannt wird:

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	Die Syntax des vorangegangenen Befehls lautet wie folgt:

	```
	add ssl certkey <Name_des_Zertifikatsschlüssels> -cert <Pfad/Name_des_Zertifikats> 	-hsmkey <Schlüsselname>
	```

	Dabei gibt `certkey` den Namen des Zertifikatsobjekts an, das in der VPX-Einheit hinzugefügt werden soll. Der Parameter `cert` enthält den Namen und den Pfad der Datei, falls sie sich nicht im aktuellen Verzeichnis befindet. Schließlich gibt `hsmkey` den Namen des Schlüssels an, der im vorherigen Schritt hinzugefügt wurde.

5.	Überprüfen Sie, ob das Zertifikat installiert wurde:

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

6.	(Optional) Um Sicherheitswarnungen beim Zugriff auf Inhalt über einen Webbrowser zu vermeiden, sollten Sie CA-Zwischenzertifikate installieren. Diese Zertifikate gestatten Citrix NetScaler VPX, Informationen mit verbundenen Clients gemeinsam zu nutzen.

	Um diese Zwischenzertifikate für RapidSSL zu erhalten, greifen Sie über einen der folgenden Links auf die entsprechende Website zu:

	* [Reissue GeoTrust Certificate For Partner Orders or QuickSSL ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [RapidSSL Intermediate and Root CA Certificates ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	Befolgen Sie die Anweisungen in diesem [Citrix-Artikel![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://support.citrix.com/article/CTX114146){:new_window}, um die Zertifikate zu installieren und zu verknüpfen.

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```
