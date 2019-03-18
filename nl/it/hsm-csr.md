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

# Creazione di chiavi e generazione di CSR (Certificate Signing Request)
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

In questa sottosezione creerai una coppia di chiavi che verrà utilizzata per generare un CSR (Certificate Signing Request) e per ordinare/richiedere un certificato con esso.

1.	Innanzitutto, conferma l'elenco di oggetti in VPX. Utilizza la password specificata per questa partizione durante la creazione.

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	```

	Questo output conferma che non esistono oggetti poiché l'output è vuoto.

	Quindi, verifica che il conteggio degli oggetti sia 0 nell'HSM visualizzando i dettagli della partizione:

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

	Il comando sopra elencato utilizza la sintassi riportata di seguito:

	```
	partition show -p <partition_name>
	```

2.	Utilizzando CMU (Certificate Management Utility) in VPX, crei una coppia di chiavi utilizzando il comando riportato di seguito. Ancora una volta, utilizza la password designata della partizione.

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	Select RSA Mechanism Type - 
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	Nella sintassi sopra riportata, il parametro `modulusBits` indica la lunghezza in bit delle chiavi RSA, mentre `publicExponent` definisce il valore esponente pubblico da utilizzare per la generazione delle chiavi, deve essere impostato su 3, 17 o 65537. La parola chiave “label” viene utilizzata per specificare una tag in modo che sia possibile identificarla e farvi facilmente riferimento in un secondo momento. Per ulteriori informazioni sugli altri due parametri o sui parametri aggiuntivi, consulta la [Utilities Reference Guide ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Conferma che gli oggetti sono stati creati. In VPX:

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	In HSM:

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

4.	Utilizzando le chiavi create nel passo precedente, genera un CSR utilizzando il programma di utilità CMU.

	Assicurati di utilizzare i valori corretti/appropriati per nome comune (CN) ed e-mail (E), il primo deve corrispondere all'FQDN che verrà utilizzato nel record A DNS associato a VPX (Virtual Server/IP). Il parametro E verrà utilizzato per inviare i dettagli di acquisto del certificato che è stato richiesto/ordinato.

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

	Nell'output sopra riportato, filename può essere qualsiasi file con un'estensione .csr, tuttavia ti consigliamo di utilizzare una descrizione significativa.

5.	Conferma la creazione del file

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
