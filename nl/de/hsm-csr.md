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

# Schlüssel erstellen und Zertifikatssignieranforderung generieren
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

In diesem Unterabschnitt wird beschrieben, wie ein Schlüsselpaar erstellt wird, das für die Generierung einer Zertifikatssignieranforderung (Certificate Signing Request, CSR) verwendet wird, und wie damit ein Zertifikat bestellt bzw. angefordert wird.

1.	Bestätigen Sie zunächst die Objektliste in VPX. Verwenden Sie das Kennwort, das während der Erstellung für diese Partition angegeben wurde.

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : 	**********
	```

	Diese Ausgabe bestätigt, dass keine Objekte vorhanden sind, da sie leer ist.

	Zeigen Sie dann die Partitionsdetails an, um zu überprüfen, ob die Objektanzahl im HSM 0 ist:

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	Partition Name:                            partition6
	Partition SN:                              534071053
	Partition Label:                           partition6
	Partition Owner Locked Out:                no
	Partition Owner PIN To Be Changed:         no
	Partition Owner Login Attempts Left:       10 before Partition Owner is Locked Out
	Legacy Domain Has Been Set:                no
	Partition Storage Information (Bytes):     Total=207559, Used=0, Free=207559
	Partition Object Count:                    0

	Command Result : 0 (Success)
	```

	Die Syntax des vorangegangenen Befehls lautet wie folgt:

	```
	partition show -p <Partitionsname>
	```

2.	Erstellen Sie mithilfe des Zertifikatsmanagementdienstprogramms (Certificate Management Utility, CMU) in VPX ein Schlüsselpaar. Verwenden Sie hierfür den nachfolgend gezeigten Befehl. Verwenden Sie wieder das angegebene Partitionskennwort.

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	Select RSA Mechanism Type - 
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	In der obigen Syntax gibt der Parameter `modulusBits` die Länge der RSA-Schlüssel in Bits an und `publicExponent` definiert den öffentlichen Exponentenwert, der für die Generierung der Schlüssel verwendet werden soll. Für diesen Wert muss 3, 17 oder 65537 angegeben werden. Mit dem Schlüsselwort 'label' wird ein Tag angegeben, durch den eine spätere Referenz oder Erkennung problemlos möglich ist. Weitere Informationen zu den beiden anderen und zu weiteren Parametern finden Sie im [Referenzhandbuch für Dienstprogramme![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Überprüfen Sie, ob Objekte erstellt wurden. In VPX:

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	Im HSM:

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	Partition Name:                            partition6
	Partition SN:                              534071053
	Partition Label:                           partition6
	Partition Owner Locked Out:                no
	Partition Owner PIN To Be Changed:         no
	Partition Owner Login Attempts Left:       10 before Partition Owner is Locked Out
	Legacy Domain Has Been Set:                no
	Partition Storage Information (Bytes):     Total=207559, Used=1660,  Free=205899
	Partition Object Count:                    2

	Command Result : 0 (Success)
	```

4.	Generieren Sie mithilfe des Zertifikatsmanagementdienstprogramms (CMU) und der im vorherigen Schritt erstellten Schlüssel eine Zertifikatssignieranforderung (CSR).

	Achten Sie darauf, dass für den allgemeinen Namen (Common Name, CN) und für die E-Mail-Adresse (E) die korrekten bzw. entsprechenden Werte verwendet werden. Der erste Wert muss mit dem vollständig qualifizierten Domänennamen (FQDN) übereinstimmen, der im A-Datensatz des DNS verwendet wird, der dem virtuellen Server/IP (VPX) zugeordnet ist. Der Parameter E wird verwendet, um die Details der Zertifikatsbeschaffung nach der Anforderung bzw. Bestellung des Zertifikats zu senden.

	```
	root@IBMADC690867-s6dr# cmu requestcertificate

	Please enter password for token in slot 0 : **********

	Enter Subject 2-letter Country Code (C) : US
	Enter Subject State or Province Name (S) : North Carolina
	Enter Subject Locality Name (L) : Durham
	Enter Subject Organization Name (O) : IBM
	Enter Subject Organization Unit Name (OU) : HSM
	Enter Subject Common Name (CN) : hsmclient7.projectgoldfinch.net   
	Enter EMAIL Address (E) : user@yourdomain.com
	Enter output filename : certreqnss6dr.csr
	```

	Der Dateiname in der oben aufgeführten Ausgabe hat die Erweiterung .csr und kann beliebig gewählt werden. Es wird jedoch eine aussagekräftige Beschreibung empfohlen.

5.	Bestätigen Sie die Erstellung der Datei.

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
