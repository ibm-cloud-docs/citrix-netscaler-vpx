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

# Instalar el software de cliente de IBM Hardware Security Module (HSM)
{: #install-the-ibm-hardware-security-module-hsm-client-software}

En este paso, se instalará Citrix VPX con el software y los programas de utilidad necesarios para interactuar con el HSM.

**NOTA:** Los pasos uno y dos de este procedimiento son opcionales y solo son necesarios si el directorio de safenet y los archivos y subcarpetas del mismo no se encuentran en la vía de acceso `/var`. Estos recursos son necesarios para que VPX se instale con el software de cliente y le permita ejecutar los programas de utilidad asociados con el software de HSM.

Busque las credenciales para acceder a la CLI de NetScaler listada en el Portal de control en **Dispositivos > Lista de dispositivos > Expandir el nombre de VPX**.

<img src="images/3-VPX-Credentials.png" alt="dibujo" style="width: 400px;"/>

Serán necesarias en esta sección y durante el resto de la guía.

**NOTA:** Tenga en cuenta que todos los resultados y mandatos de VPX de este documento mostrarán `netscalername#` (indicando una ejecución de shell) o `>` (para la misma CLI de VPX).

1.	(OPCIONAL) Obtenga el archivo `safenet_dirs.tar` y transfiéralo a la VPX en el directorio `/var`. El archivo `safenet_dirs.tar` se puede obtener [aquí ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window}.

	**NOTA:** Debe haber iniciado sesión en la cuenta de SoftLayer para acceder al enlace anterior.

	<img src="images/4-transfer-safenet_dirs.png" alt="dibujo" style="width: 600px;"/>

	Esta imagen muestra el software de WinSCP que transfiere el archivo `safenet_dir.tar` a Citrix VPX.

2.	(OPCIONAL) Extraiga el archivo `tar`:

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

3.	Vaya al directorio `/var/safenet` y confirme que las carpetas y archivos se han transferido:

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	Ejecute el script de instalación utilizando la versión 622:

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

5.	Confirme la creación del directorio safenet:

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	Vaya al directorio `/var/safenet/config/` y ejecute el script `safenet_config`:

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	Compruebe que `/etc/Chrystoki.conf` y el enlace simbólico `/usr/lib/libCrystoki_64` se hayan creado:

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

IBM© Hardware Security Module se ha instalado correctamente.
