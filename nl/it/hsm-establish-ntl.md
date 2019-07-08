---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: security, hsm, ntl, certificate

subcollection: citrix-netscaler-vpx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Come stabilire un NTL (Network Trust Link)
{: #establish-a-network-trust-link-ntl-}

Un NTL (Network Trust Link) è un canale sicuro utilizzato da HSM (Hardware Security Module) e dal client per comunicare. NTL utilizzano certificati in entrambe le direzioni per autenticare e crittografare i dati trasmessi tra le partizioni server HSM e i client.

Tieni presente che Trust Link richiede che la porta 1792 TCP sia accessibile in entrambi i protocolli NTLS e NTLA (bidirezionali) per garantire che tutti i processi e i programmi di utilità funzionino correttamente.

Per stabilire il tuo NTL, esegui la seguente procedura:

1.	Passa alla directory `/var/safenet/safenet/lunaclient/bin` e crea il certificato utilizzando il programma di utilità VTL.

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	Private Key created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	Certificate created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**NOTA:** l'identificativo utilizzato per il certificato client è l'IP privato assegnato ad esso. HSM lo utilizzerà e vi farà riferimento successivamente.

2. Trasferisci il file del certificato nel server HSM utilizzando SCP:

	```
	root@IBMADC690867-s6dr# scp /var/safenet/safenet/lunaclient/cert/client/	10.121.229.224.pem hsm_admin@10.121.229.201:

	The authenticity of host '10.121.229.201 (10.121.229.201)' can't be established.

	ECDSA key fingerprint is SHA256:UBltOfaDojRlUVxDXh6zI3CPMF8FRaJnls0uxeWgrCY.

	Are you sure you want to continue connecting (yes/no)? yes

	Warning: Permanently added '10.121.229.201' (ECDSA) to the list of known hosts.

	hsm_admin@10.121.229.201's password:

	10.121.229.224.pem                                                 
	100%  818     	
	1.6MB/s   
	00:00
	```

	Per ulteriori informazioni su VTL (Virtual Token Library), vai alla [Utilities Reference Guide ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Trasferisci il file del certificato del server HSM al client Citrix Netscaler VPX utilizzando SCP, quindi aggiungi il server:

	```
	root@IBMADC690867-s6dr# scp hsm_admin@10.121.229.201:server.pem .
	hsm_admin@10.121.229.201's password:

	server.pem                                                         
	100% 1180     	
	2.3MB/s   
	00:00

	root@IBMADC690867-s6dr# vtl addServer -n 10.121.229.201 -c server.pem

	Il nuovo server 10.121.229.201 è stato aggiunto correttamente all'elenco di server.
	```

	La sintassi sopra utilizzata è la seguente:

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. Conferma l'aggiunta del server:

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	In HSM, esegui il seguente comando per vedere i client esistenti:

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs

	Command Result : 0 (Success)
	```

5.	Registra VPX come nuovo client:

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	'client register' successful.

	Command Result : 0 (Success)
	```

	Il precedente comando utilizza la seguente sintassi:

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	Il nome client non deve corrispondere all'identificativo assegnato e utilizzato da IBM© Cloud, tuttavia, si consiglia di mantenere i nomi coerenti.

6. Conferma che il client è stato aggiunto:

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs
	registered client 6: NS-IBMADC690867-s6dr

	Command Result : 0 (Success)
	```

7. Assegna una partizione al client. Assicurati di fare riferimento alla partizione creata in precedenza. Devi anche assicurarti che il nome corrisponda all'identificativo del client visualizzato nel passo precedente.

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition' successful.

	Command Result : 0 (Success)
	```

	L'output precedente utilizza la seguente sintassi:

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	Verifica la connettività nel tuo Citrus Netscaler VPX:

	```
	root@IBMADC690867-s6dr# vtl verify

	Sono stati trovati i seguenti Slot/Partizioni Luna SA:

	Slot    Serial #                Label
	====    ================        =====
	0           534071053        partition6
	```

	L'output visualizzato da `vtl verify` deve elencare "Slot #", numero di serie e nome della partizione associata a questo Trust Link. Qualsiasi altro output indica un problema.

	Inoltre, ti consigliamo di confermare i percorsi dei certificati e il server nel file Chrystoki ch si trova nella directory `/etc`. Per eseguire tale operazione:

	```
	root@IBMADC690867-s6dr# cd /etc/
	root@IBMADC690867-s6dr# cat /etc/Chrystoki.conf
	Chrystoki2 = {
		LibUNIX64 = /var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so;
		}

	[OUTPUT OMMITED]
		ClientPrivKeyFile = /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem;
		ClientCertFile = /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem;
		ServerCAFile = /var/safenet/safenet/lunaclient/cert/server/CAFile.pem;
		NetClient = 1;
		HtlDir = /var/safenet/safenet/lunaclient/htl/;
		ServerName00 = 10.121.229.201;
		ServerPort00 = 1792;
		ServerHtl00 = 0;
	}
	[OUTPUT OMITTED]
	```

9.	Salva la configurazione:

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	Il comando copy qui utilizzato rende persistente la configurazione tra i riavvi in VPX.

10.	Avvia il processo client del gateway safenet necessario per le operazioni di crittografia:

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. Conferma che il processo è in esecuzione:

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. Infine, assicurati che questo processo venga avviato automaticamente durante il processo di riavvio:

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

Ora hai stabilito il tuo NTL (Network Trust Link).
