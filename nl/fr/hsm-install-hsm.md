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

# Installation du logiciel client du module de sécurité matérielle IBM HSM (Hardware Security Module)
{: #install-the-ibm-hardware-security-module-hsm-client-software}

Dans cette étape, Citrix VPX sera installé avec le logiciel et les utilitaires requis pour interagir avec le module HSM.

**Remarque :** Les étapes 1 et 2 de cette procédure sont facultatives et nécessaires uniquement si le répertoire safenet et les fichiers ou sous-dossiers qu'il contient sont manquants dans le chemin `/var`. Ces ressources sont nécessaires pour l'installation de VPX avec le logiciel client et lui permettent d'exécuter les utilitaires associés au logiciel HSM.

Recherchez les données permettant d'accéder à l'interface CLI de NetScaler dans le portail de contrôle sous **Devices > Device List > Expand VPX name**.

<img src="images/3-VPX-Credentials.png" alt="dessin" style="width: 400px;"/>

Elles seront nécessaires pour la présente section et pour le reste du guide.

**Remarque :** Veuillez noter que toutes les commandes VPX et sorties de ce document afficheront `netscalername#` (indiquant l'exécution du shell ou `>` pour l'interface CLI VPX elle-même).

1.	(Facultatif) Recherchez le fichier `safenet_dirs.tar` et transférez-le vers le VPX dans le répertoire `/var`. Le fichier `safenet_dirs.tar` peut être obtenu [ici![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window}.

	**Remarque :** Vous devez être connecté à votre compte SoftLayer pour pouvoir accéder au lien dessus.

	<img src="images/4-transfer-safenet_dirs.png" alt="dessin" style="width: 600px;"/>

	Cette image illustre le transfert du fichier `safenet_dir.tar` vers Citrix VPX à l'aide du logiciel WinSCP.

2.	(Facultatif) Extrayez le contenu du fichier `tar` :

	```
	root@IBMADC690867-wnzs# tar -xvpf safenet_dirs.tar
	x safenet/
	x safenet/config/
	x safenet/gateway/
	x safenet/SAClient_600.tgz
	x safenet/SAClient_622.tgz
	x safenet/install_client.sh
	x safenet/gateway/start_safenet_gw
	x safenet/gateway/gw_delay
	x safenet/config/safenet_config
	x safenet/config/Chrystoki.conf
	```

3.	Accédez au répertoire `/var/safenet` et vérifiez que les dossiers et les fichiers ont été transférés :

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	Exécutez le script d'installation à l'aide de la version 622 :

	```
	root@IBMADC690867-s6dr# install_client.sh -v 622
	*********************************************
	Current Version: 622
	Installing Version: 622
	Starting to extract SAClient_622.tgz file.
	Extracted SAClient_622.tgz file.
	Removing SAClient_622.tgz file.

	*********************************************

	Now follow the configuration steps document available online on Citrix edocs.
	*********************************************
	```

5.	Confirmez la création du répertoire safenet :

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	Accédez au répertoire `/var/safenet/config/` et exécutez le script `safenet_config` :

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	Vérifiez que `/etc/Chrystoki.conf` et le lien symbolique `/usr/lib/libCrystoki_64` ont été créés :

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

IBM© Hardware Security Module a été installé avec succès.
