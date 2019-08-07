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

# Neue Cipher-Suite erstellen und anwenden
{: #create-and-apply-a-new-cipher-suite}

Eine Cipher-Suite ist eine Kombination aus Authentifizierung, Verschlüsselung, Nachrichtenauthentifizierungscode und Schlüsselaustauschalgorithmen, mit der die Sicherheitseinstellungen für SSL-und TLS-Protokolle vereinbart werden.

Um eine ordnungsgemäße Authentifizierung zu gewährleisten, müssen Sie sicherstellen, dass Ihre {{site.data.keyword.vpx_full}}-Instanz die beste Kombination der Verschlüsselungsverfahren verwendet.

Weitere Informationen zu SSL-Cipher-Suites und andere Best Practices finden Sie auf den folgenden Websites:

* [Scoring an A+ at SSLlabs.com with Citrix NetScaler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.citrix.com/blogs/2018/05/16/scoring-an-a-at-ssllabs-com-with-citrix-netscaler-q2-2018-update/){:new_window} – Q2 2018 update (siehe Schritt 3 und 5 im Befehlsabschnitt)
* [SSL and TLS Deployment Best Practices ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices#23-use-secure-cipher-suites){:new_window}
* [How Do I Setup ECC on NetScaler? ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://support.citrix.com/article/CTX205289){:new_window}

**HINWEIS:** Die Ausführungen in diesem Abschnitt konzentrieren sich auf bestimmte und erforderliche Konfigurationen für SSL-Verschlüsselungen. Die Informationen, die Sie über die vorangegangenen Links finden können, enthalten möglicherweise zusätzliche Einstellungen, die zur Optimierung des SSL-Verfahrens angewendet werden können.

Gehen Sie wie folgt vor, um eine neue Cipher-Suite zu erstellen, die AEAD-, ECDHE- und ECDSA-Chiffrierwerte priorisiert:

1.	Geben Sie die folgenden Befehle gleichzeitig in die Citrix VPX-Befehlszeilenschnittstelle ein und stellen Sie sicher, dass sie alle angewendet werden.

	```
	add ssl cipher SSLLABS
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-256-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-256-CBC-SHA
	```

	Die Syntax der vorangegangenen Befehle lautet wie folgt:

	```
	add ssl cipher <Name_der_Chiffrierwertgruppe>
	bind ssl cipher <Name_der_Chiffrierwertgruppe> -cipherName <Zeichenfolge>
	```

2.	Überprüfen Sie, ob der Chiffrierwert Ihrer {{site.data.keyword.vpx_full}}-Instanz hinzugefügt wurde:

	```
	> show ssl cipher SSLLABS
	1)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256       Priority : 1
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02b
	2)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384       Priority : 2
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc02c
	3)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES128-SHA256   Priority : 3
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA-256   HexCode=0xc023
	4)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES256-SHA384   Priority : 4
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA-384   HexCode=0xc024
	5)      Cipher Name: TLS1-ECDHE-ECDSA-AES128-SHA        Priority : 5
	        Description: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA1   HexCode=0xc009
	6)      Cipher Name: TLS1-ECDHE-ECDSA-AES256-SHA        Priority : 6
	        Description: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA1   HexCode=0xc00a
	7)      Cipher Name: TLS1.2-ECDHE-RSA-AES128-GCM-SHA256 Priority : 7
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02f
	8)      Cipher Name: TLS1.2-ECDHE-RSA-AES256-GCM-SHA384 Priority : 8
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc030
	9)      Cipher Name: TLS1.2-ECDHE-RSA-AES-128-SHA256    Priority : 9
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA-256   HexCode=0xc027
	10)     Cipher Name: TLS1.2-ECDHE-RSA-AES-256-SHA384    Priority : 10
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA-384   HexCode=0xc028
	11)     Cipher Name: TLS1-ECDHE-RSA-AES128-SHA  Priority : 11
	        Description: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0xc013
	12)     Cipher Name: TLS1-ECDHE-RSA-AES256-SHA  Priority : 12
	        Description: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0xc014
	13)     Cipher Name: TLS1.2-DHE-RSA-AES128-GCM-SHA256   Priority : 13
	        Description: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0x009e
	14)     Cipher Name: TLS1.2-DHE-RSA-AES256-GCM-SHA384   Priority : 14
	        Description: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0x009f
	15)     Cipher Name: TLS1-DHE-RSA-AES-128-CBC-SHA       Priority : 15
	        Description: SSLv3 Kx=DH       Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x0033
	16)     Cipher Name: TLS1-DHE-RSA-AES-256-CBC-SHA       Priority : 16
	        Description: SSLv3 Kx=DH       Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0039
	17)     Cipher Name: TLS1-AES-128-CBC-SHA       Priority : 17
	        Description: SSLv3 Kx=RSA      Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x002f
	18)     Cipher Name: TLS1-AES-256-CBC-SHA       Priority : 18
	        Description: SSLv3 Kx=RSA      Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0035
 	Done
 	```

3.	Heben Sie die Bindung der Standard-Cipher-Suite an Ihren virtuellen Server auf und binden Sie die im vorangegangenen Schritt erstellte angepasste Gruppe:

	```
	unbind ssl vserver https_vip2 -cipherName DEFAULT

	bind ssl vserver https_vip2 -cipherName SSLLABS

	bind ssl vserver https_vip2 -eccCurveName ALL
	```

	Die Syntax der vorangegangenen Befehle lautet wie folgt:

	```
	unbind ssl cipher <Name_der_Chiffrierwertgruppe> -cipherName <Zeichenfolge>
	bind ssl vserver <Name_des_virt._Servers> -cipherName <Zeichenfolge>
	bind ssl vserver <Name_des_virt._Servers> -eccCurveName <Name_der_ECC-Kurve>
	```

4.	Überprüfen Sie die Änderungen in Ihrem virtuellen Server:

	```
	> show ssl vserver https_vip2

	[OUTPUT OMITTED]
		ECC Curve: P_256, P_384, P_224, P_521

	1)      CertKey Name: hsmclient7ns      Server Certificate

	1)      Cipher Name: SSLLABS
		Description: User Created Cipher Group
 	Done
	```

5.	(Optional) HTTP-Weiterleitung kann aktiviert werden, um Benutzer auf eine sichere Website weiterzuleiten, wenn sie eine HTTP-Anforderung (keine HTTPS-Anforderung) erstellen.

	Konfigurationsanweisungen finden Sie unter [Konfiguration der Weiterleitung von HTTP nach HTTPS in NetScaler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://support.citrix.com/article/CTX201201){:new_window}.

6. Testen Sie die HTTPS-Verbindung, indem Sie einen Webbrowser öffnen und den FQDN eingeben. Auf der Website sollte der Inhalt geladen werden, der von dem HTTP-Service hinter dem Citrix VPX wiedergegeben wird.

	Sie können auch die Zertifikatsdetails anzeigen. Klicken Sie hierfür auf das Schlosssymbol neben der URL in Ihrem Browser, um die Zertifikatsinformationen anzuzeigen.

	<img src="images/21-check-certificate.png" alt="drawing" style="width: 350px;"/>

	Wurde die Weiterleitung in Schritt 5 konfiguriert, wird die sichere Site auch bei Verwendung einer HTTP-Anforderung geladen.
