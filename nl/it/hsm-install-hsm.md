---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, install

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

# Installazione del software client IBM Hardware Security Module (HSM)
{: #install-the-ibm-hardware-security-module-hsm-client-software}

In questo passo, Citrix VPX verrà installato con il software e i programmi di utilità richiesti per interagire con HSM.

I passi uno e due di questa procedura sono facoltativi e sono necessari solo se la directory safenet e i file o le sottocartelle contenuti in essa non sono presenti nel percorso `/var`. Queste risorse sono necessarie per installare VPX con il software client e gli consentono di eseguire i programmi di utilità associati al software HSM.
{: note}

Trova le credenziali per accedere alla CLI NetScaler elencate nel portale di controllo in **Devices > Device List > Expand VPX name**.

<img src="images/3-VPX-Credentials.png" alt="immagine" style="width: 400px;"/>

Saranno necessarie per questa sezione e per il resto della guida.

Tieni presente che tutti i comandi VPX e gli output presenti in questo documento elencheranno `netscalername#` (indicante un'esecuzione shell) oppure `>` (per la CLI VPX stessa).
{: note}

1.	(FACOLTATIVO) Ottieni il file `safenet_dirs.tar` e trasferiscilo a VPX nella directory `/var`. Puoi ottenere il file `safenet_dirs.tar` da [qui ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window}.

	Devi essere collegato al tuo account SoftLayer per accedere al link sopra riportato.
  {: note}

	<img src="images/4-transfer-safenet_dirs.png" alt="immagine" style="width: 600px;"/>

	Questa immagine mostra il software WinSCP che trasferisce il file `safenet_dir.tar` nel Citrix VPX.

2.	(FACOLTATIVO) Estrai il file `tar`:

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

3.	Passa alla directory `/var/safenet` e conferma che le cartelle e i file sono stati trasferiti:

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	Esegui lo script di installazione utilizzando la versione 622:

	```
	root@IBMADC690867-s6dr# install_client.sh -v 622
	*********************************************
	Current Version: 622
	Installing Version: 622
	Starting to extract SAClient_622.tgz file.
	Extracted SAClient_622.tgz file.
	Removing SAClient_622.tgz file.

	*********************************************

	Ora segui il documento contenente i passi di configurazione disponibile online nelle edocs Citrix.
	*********************************************
	```

5.	Conferma la creazione della directory safenet:

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	Passa alla directory `/var/safenet/config/` ed esegui lo script `safenet_config`:

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	Verifica che siano stati creati `/etc/Chrystoki.conf` e il link simbolico `/usr/lib/libCrystoki_64`:

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

IBM© Hardware Security Module è stato installato correttamente.
