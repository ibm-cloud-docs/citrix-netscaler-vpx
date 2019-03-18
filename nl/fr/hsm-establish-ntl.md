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

# Etablir un lien de confiance de réseau (NTL)
{: #establish-a-network-trust-link-ntl-}

Un lien de confiance de réseau (NTL) est un canal de communication sécurisé entre le module de sécurité matérielle HSM (Hardware Security Module) et le client. Les liens NTL utilisent des certificats dans les deux sens pour pouvoir authentifier et chiffrer les données transmises entre les partitions du serveur et les clients.

Notez que le lien de confiance nécessite que le port TCP 1792 soit accessible dans les protocoles NTLS et NTLA (bidirectionnels) pour garantir le bon fonctionnement de tous les processus et utilitaires.

Pour établir la connexion NTL, procédez comme suit :

1.	Accédez au répertoire `/var/safenet/safenet/lunaclient/bin` et créez le certificat à l'aide de l'utilitaire VTL.

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	Private Key created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	Certificate created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**Remarque :** L'identificateur utilisé pour le certificat client correspond à l'adresse IP privée qui lui est attribuée. Celui-ci sera utilisé et référencé ultérieurement par HSM.

2. Transférez le fichier certificat au serveur HSM via SCP :

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

	Pour en savoir plus sur la bibliothèque de jetons virtuels (VTL), consultez le document [Utilities Reference Guide (en anglais) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Transférez le fichier certificat du serveur HSM vers le client Citrix NetScaler VPX via SCP, puis ajoutez le serveur :

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

	La syntaxe utilisée dans l'exemple ci-dessus est la suivante :

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. Vérifiez que le serveur a été ajouté :

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	Dans HSM, exécutez la commande suivante pour afficher tous les clients existants :

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs

	Command Result : 0 (Success)
	```

5.	Enregistrez le VPX en tant que nouveau client :

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	'client register' successful.

	Command Result : 0 (Success)
	```

	La commande ci-dessus utilise la syntaxe suivante :

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	Le nom du client ne doit pas nécessairement correspondre à l'identificateur attribué et utilisé par IBM© Cloud. Toutefois, il est recommandé d'utiliser une méthode d'attribution de noms qui soit cohérente.

6. Vérifiez que le client a bien été ajouté :

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

7. Affectez une partition au client. Assurez-vous de faire référence à la partition créée auparavant. Vous devrez également vérifier que le nom correspond à l'identifiant du client affiché à l'étape précédente.

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition' successful.

	Command Result : 0 (Success)
	```

	La sortie ci-dessus respecte la syntaxe suivante :

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	Vérifiez la connectivité dans votre Citrix NetScaler VPX :

	```
	root@IBMADC690867-s6dr# vtl verify

	The following Luna SA Slots/Partitions were found:

	Slot    Serial #                Label
	====    ================        =====
	0           534071053        partition6
	```

	La sortie générée par la commande `vtl verify` doit indiquer le numéro d'emplacement de la partition, le numéro de série et le nom de la partition associée au lien de confiance. Tout autre résultat indique un problème.

	En outre, il peut être judicieux de vérifier le chemin des certificats et du serveur dans le fichier Chrystoki situé dans le répertoire `/etc`. Pour ce faire :

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

9.	Enregistrez la configuration :

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	La commande de copie utilisée ici rend la configuration persistante lors des redémarrages dans VPX.

10.	Démarrez le processus client de la passerelle safenet nécessaire aux opérations cryptographiques :

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. Vérifiez que le processus est en cours d'exécution :

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. Enfin, assurez-vous que le processus démarre automatiquement lors du processus de redémarrage :

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

Votre connexion NTL est maintenant établie.
