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

# Establecer un enlace de confianza de red (NTL)
{: #establish-a-network-trust-link-ntl-}

Un enlace de confianza de red (NTL) es un canal seguro para que el gestor de servicios de hardware (HSM) y el cliente se comuniquen. Los enlaces de confianza de red utilizan certificados en ambas direcciones para autenticar y cifrar datos transmitidos entre las particiones de servidor HSM y los clientes.

Tenga en cuenta que el enlace de confianza requiere que el puerto TCP 1792 sea accesible en los protocolos NTL y NTLA (bidireccional) para garantizar que todos los procesos y programas de utilidad funcionen correctamente.

Para establecer el enlace de confianza de red, realice el procedimiento siguiente:

1.	Vaya al directorio `/var/safenet/safenet/lunaclient/bin` y cree el certificado utilizando el programa de utilidad VTL.

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	Private Key created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	Certificate created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**NOTA:** El identificador utilizado para el certificado de cliente es la IP privada asignada al mismo. Esto se utilizará posteriormente y el HSM hará referencia al mismo.

2. Transfiera el archivo de certificado al servidor de HSM utilizando el SCP:

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

	Para obtener más información sobre la biblioteca virtual de cintas (VTL), vaya a la [Guía de referencia de los programas de utilidad ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Transfiera el archivo de certificado del servidor HSM al cliente {{site.data.keyword.vpx_full}} utilizando el SCP y, a continuación, añada el servidor:

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

	La sintaxis utilizada anteriormente es la siguiente:

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. Confirme la adición del servidor:

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	En el HSM, ejecute el mandato siguiente para ver los clientes existentes:

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs

	Command Result : 0 (Success)
	```

5.	Registre el VPX como nuevo cliente:

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	'client register' successful.

	Command Result : 0 (Success)
	```

	El mandato anterior utiliza la sintaxis siguiente:

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	El nombre de cliente no tiene que coincidir con el identificador asignado y utilizado por IBM© Cloud; sin embargo, se recomienda que los nombres sean coherentes.

6. Confirme que se ha añadido el cliente:

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

7. Asigne una partición al cliente. Asegúrese de que hace referencia a la partición creada anteriormente. También tendrá que asegurarse de que el nombre coincide con el identificador del cliente mostrado en el paso anterior.

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition' successful.

	Command Result : 0 (Success)
	```

	El resultado anterior utiliza la sintaxis siguiente:

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	Verifique la conectividad en Citrus Netscaler VPX:

	```
	root@IBMADC690867-s6dr# vtl verify

	The following Luna SA Slots/Partitions were found:

	Slot    Serial #                Label
	====    ================        =====
	0           534071053        partition6
	```

	El resultado mostrado por `vtl verify` debe enumerar el número de ranura ("Slot #"), el número de serie y el nombre del enlace de partición en este enlace de confianza. Cualquier otro resultado indica un problema.

	Además, también se recomienda confirmar las vías de acceso de los certificados y el servidor en el archivo Chrystoki ubicado en el directorio `/etc`. Para ello, realice lo siguiente:

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

9.	Guarde la configuración:

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	El mandato de copia que se utiliza aquí hace que la configuración sea persistente entre rearranques en VPX.

10.	Inicie el proceso del cliente de pasarela de safenet necesario para las operaciones criptográficas:

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. Confirme que el proceso se está ejecutando:

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. Por último, asegúrese de que el proceso se inicia automáticamente durante el proceso de rearranque:

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

Se ha establecido el enlace de confianza de red (NTL).
