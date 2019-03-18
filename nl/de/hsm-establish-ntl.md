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

# Network Trust Link (NTL) aufbauen
{: #establish-a-network-trust-link-ntl-}

Ein Network Trust Link (NTL) ist ein sicherer Kanal für die Kommunikation zwischen dem Hardware Security Module (HSM) und dem Client. NTLs verwenden Zertifikate in beiden Richtungen, um Daten, die zwischen HSM-Serverpartitionen und Clients übertragen werden, zu authentifizieren und zu verschlüsseln.

Es ist zu beachten, dass für den Trust-Link der Zugriff auf TCP-Port 1792 sowohl im NTLS- als auch im NTLA-Protokoll (bidirektional) möglich sein muss, um sicherzustellen, dass alle Prozesse und Dienstprogramme korrekt funktionieren.

Gehen Sie wie folgt vor, um den NTL einzurichten:

1.	Wechseln Sie in das Verzeichnis `/var/safenet/safenet/lunaclient/bin` und erstellen Sie das Zertifikat mithilfe des Dienstprogramms VTL.

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	Private Key created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	Certificate created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**HINWEIS:** Die für das Clientzertifikat verwendete ID ist die ihm zugeordnete private IP. Sie wird später vom HSM verwendet und referenziert.

2. Übertragen Sie die Zertifikatsdatei mit SCP an den HSM-Server:

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

	Weitere Informationen zu Virtual Token Library (VTL) finden Sie im [Referenzhandbuch für Dienstprogramme ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Übertragen Sie die HSM-Serverzertifikatsdatei mit SCP an den Citrix NetScaler VPX-Client und fügen Sie dann den Server hinzu:

	```
	root@IBMADC690867-s6dr# scp hsm_admin@10.121.229.201:server.pem .
	hsm_admin@10.121.229.201's password:

	server.pem                                                         
	100% 1180     	
	2.3MB/s   
	00:00

	root@IBMADC690867-s6dr# vtl addServer -n 10.121.229.201 -c server.pem

	New server 10.121.229.201 successfully added to server list.
	```

	Die im vorangegangenen Abschnitt verwendete Syntax lautet wie folgt:

	```
	vtl addServer -n <SA-Hostname_oder_-IP> -c <Serverzertifikat>
	```

3. Bestätigen Sie das Hinzufügen des Servers:

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	Führen Sie im HSM den folgenden Befehl aus, um alle vorhandenen Clients anzuzeigen:

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs

	Command Result : 0 (Success)
	```

5.	Registrieren Sie den VPX als neuen Client:

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	'client register' successful.

	Command Result : 0 (Success)
	```

	Die Syntax des vorangegangenen Befehls lautet wie folgt:

	```
	client register -client <Clientname> -ip <Client-IP-Adresse>
	```

	Der Clientname muss nicht mit der von IBM© Cloud zugeordneten und verwendeten ID übereinstimmen, eine Übereinstimmung wird jedoch empfohlen, um die Namen konsistent zu halten.

6. Überprüfen Sie, ob der Client hinzugefügt wurde:

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

7. Ordnen Sie dem Client eine Partition zu. Stellen Sie sicher, dass Sie auf die zuvor erstellte Partition verweisen. Darüber hinaus müssen Sie sicherstellen, dass der Name mit der im vorherigen Schritt angezeigten ID des Clients übereinstimmt.

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition' successful.

	Command Result : 0 (Success)
	```

	Die Syntax der vorangegangenen Ausgabe lautet wie folgt:

	```
	client assignPartition -client <Clientname> -partition <Partitionsname>
	```

8.	Überprüfen Sie die Konnektivität in Ihrer Citrix NetScaler VPX-Instanz:

	```
	root@IBMADC690867-s6dr# vtl verify

	The following Luna SA Slots/Partitions were found:

	Slot    Serial #                Label
	====    ================        =====
	0           534071053        partition6
	```

	In der Ausgabe des Befehls `vtl verify` sollte der Bereich (Slot), die Seriennummer (Serial #) und der Name (Label) der Partition, die an diesen Trust-Link gebunden ist, aufgelistet sein. Jede andere Ausgabe weist auf ein Problem hin.

	Außerdem wird empfohlen, die Pfade der Zertifikate und des Servers in der Chrystoki-Datei im Verzeichnis `/etc` zu bestätigen. Gehen Sie hierfür wie folgt vor:

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

9.	Speichern Sie die Konfiguration:

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	Durch den hier verwendeten Kopierbefehl bleibt die Konfiguration auch nach Neustarts in VPX persistent.

10.	Starten Sie den SafeNet-Gateway-Clientprozess, der für Verschlüsselungsoperationen erforderlich ist:

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. Überprüfen Sie, ob der Prozess ausgeführt wird:

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. Schließlich müssen Sie sicherstellen, dass dieser Prozess während des Neustarts automatisch gestartet wird:

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

Der NTL ist jetzt eingerichtet.
