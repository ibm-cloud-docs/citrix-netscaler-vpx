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

# SSL-Zertifikat bestellen
{: #order-an-ssl-certificate}

Secure Sockets Layer (SSL) ist eine Technologie, die den Datenverkehr zwischen der Clientanwendung und der Serveranwendung verschlüsselt und mit einem aus einem öffentlichen Schlüssel/privaten Schlüssel bestehenden System, das ein SSL-Zertifikat verwendet, ausgeführt wird.

SSL-Zertifikate enthalten den öffentlichen Schlüssel des Servers, die Datumsangaben für die Gültigkeit des Zertifikats, einen Hostnamen, für den das Zertifikat gültig ist, und eine Signatur von der Zertifizierungsstelle, die das Zertifikat ausgestellt hat.

IBM© Cloud bietet Zertifikate an, die angefordert und gekauft werden können, ohne dafür einen anderen Anbieter/eine andere Site in Anspruch nehmen zu müssen.

IBM Cloud bietet jährliche und halbjährliche SSL-Zertifikate für Kunden an, die verschiedene Vorteile bieten. Dazu gehören:

* Vollständige Authentifizierung für die Prüfung der Geschäftsidentität und des Domäneneigentums
* 40- bis 256-Bit-Verschlüsselung bei allen Onlinetransaktionen
* Täglicher Website-Malware-Scan, um sicherzustellen, dass sowohl Ihre Website als auch Ihre Kunden geschützt sind

Wenn Sie mehrere Domänen betreiben, kann ein SSL-Zertifikat für jede Domäne gekauft werden.

Weitere Informationen zu SSL-Zertifikaten finden Sie in den folgenden IBM Cloud-Artikeln:

* [Informationen zu SSL-Zertifikaten](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [Einführung in die SSL-Technologie](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [Planung für SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)


Gehen Sie wie folgt vor, um ein SSL-Zertifikat für die Verwendung mit {{site.data.keyword.vpx_full}} zu bestellen:

1.	Zeigen Sie in der Befehlszeilenschnittstelle der VPX-Shell den CSR-Text an, indem Sie die in Schritt [Schlüssel erstellen und Zertifikatssignieranforderung generieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) erstellte CSR-Datei öffnen:

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

2.	Kopieren Sie den Inhalt der Datei ab `---BEGIN NEW CERTIFICATE REQUEST---` bis `---END NEW CERTIFICATE REQUEST---`.

3.	[Führen Sie diese Anweisungen aus](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates), um die Bestellung aufzugeben. Fügen Sie dabei den Text aus der CSR-Datei in das entsprechende Feld ein. Im folgenden Beispiel wurde `RapidSSL 1 Year` ausgewählt.

	<img src="images/5-Order-Certificate_1.png" alt="Zeichnung" style="width: 550px;"/>

	Wie gezeigt, verarbeitet und interpretiert das System den CSR-Text und zeigt ihn anschließend auf der folgenden Seite an.

	Stellen Sie sicher, dass ein gültiges E-Mail-Konto und eine gültige Domäne/Unterdomäne ausgewählt werden, da diese Methode für die Validierung des Domäneneigentumsrechts festgelegt ist.

	Bestätigen Sie Ihre Bestelldetails und klicken Sie auf **Bestellung aufgeben**.

4. Sie erhalten eine Bestellbestätigung mit den Details der Zertifikatsanforderung für das angegebene Konto.

	Klicken Sie auf den in der E-Mail enthaltenen Link, um die Domänenvalidierungsanforderung zu genehmigen. An diesem Punkt sollte die SSL-Anforderung bereit sein, um mit der Auftragserfüllung beginnen zu können.
