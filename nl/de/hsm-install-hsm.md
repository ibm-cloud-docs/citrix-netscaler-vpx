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

# Client-Software für IBM Hardware Security Module (HSM) installieren
{: #install-the-ibm-hardware-security-module-hsm-client-software}

In diesem Schritt wird Citrix VPX mit der Software und den Dienstprogrammen installiert, die für die Interaktion mit dem HSM erforderlich sind.

**HINWEIS:** Die Schritte 1 und 2 in dieser Prozedur sind optional und müssen nur ausgeführt werden, wenn das Verzeichnis 'safenet' und die darin enthaltenen Dateien oder Unterordner im Pfad `/var` fehlen. Diese Ressourcen sind erforderlich, damit VPX mit der Client-Software installiert werden kann, und sie ermöglichen die Ausführung der zur HSM-Software gehörigen Dienstprogramme.

Die Berechtigungsnachweise für den Zugriff auf die NetScaler-Befehlszeilenschnittstelle sind im Steuerungsportal unter **Einheiten > Einheitenliste > VPX-Namen einblenden** aufgelistet.

<img src="images/3-VPX-Credentials.png" alt="Zeichnung" style="width: 400px;"/>

Sie werden für diesen Abschnitt und für die restliche Anleitung benötigt.

**HINWEIS:** Beachten Sie, dass bei allen VPX-Befehlen und -Ausgaben in diesem Dokument entweder `netscalername#` (zeigt eine Shellausführung an) oder `>` (für die VPX-Befehlszeilenschnittstelle selbst) aufgelistet wird.

1.	(Optional) Rufen Sie die Datei `safenet_dirs.tar` ab und übertragen Sie sie in das VPX-Verzeichnis `/var`. Die Datei `safenet_dirs.tar` kann [hier ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window} abgerufen werden.

	**HINWEIS:** Sie müssen bei Ihrem SoftLayer-Konto angemeldet sein, um auf den obigen Link zugreifen zu können.

	<img src="images/4-transfer-safenet_dirs.png" alt="Zeichnung" style="width: 600px;"/>

	Diese Abbildung zeigt, wie die WinSCP-Software die Datei `safenet_dir.tar` in das Citrix VPX-Verzeichnis überträgt.

2.	(Optional) Extrahieren Sie die `tar`-Datei:

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

3.	Wechseln Sie in das Verzeichnis `/var/safenet` und überprüfen Sie, ob die Ordner und Dateien übertragen wurden.

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	Führen Sie das Installationsscript mit Version 622 aus:

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

5.	Bestätigen Sie die Erstellung des Verzeichnisses 'safenet':

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	Wechseln Sie in das Verzeichnis `/var/safenet/config/` und führen Sie das Script `safenet_config` aus:

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	Überprüfen Sie, ob `/etc/Chrystoki.conf` und der symbolische Link `/usr/lib/libCrystoki_64` erstellt wurden:

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

Die Installation von IBM© Hardware Security Module war erfolgreich.
