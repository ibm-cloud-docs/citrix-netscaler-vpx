---

copyright:
  years: 2019
lastupdated: "2019-04-10"

keywords: ipsec, vpn, vpx, tunnel

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

# Creación de un túnel de IP
{: #creating-ip-tunnel}

Tiene que crear un objeto de túnel de IP para especificar no sólo las direcciones IP locales y remotas, sino también los parámetros de protocolo de la conexión VPN. Para ello, realice lo siguiente:

1.	Vaya a **Sistema > CloudBridge Connector > Túneles de IP**.
2.	En el **separador Túneles de IPv4**, pulse **Añadir**.
3.	Especifique los parámetros siguientes:
  *	Nombre
  *	IP remota (IP del homólogo de VPN remoto)
  *	Máscara remota
4.	Seleccione **IP de subred** (SNIP) en la lista desplegable IP local.
5.	Elija el SNIP adecuado para utilizar como punto final de VPN en el desplegable **IP local**.
6.	Seleccione el protocolo **IPSEC** en la lista desplegable.
7.	Elija el nombre de perfil [creado anteriormente](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) en el desplegable **nombre de perfil de IPSec**. 
8.	Pulse **Crear**.

    <img src="images/ipsecCreateIPtunnel.png" alt="dibujo" style="width: 200px;"/>

Para crear un túnel de IP en la CLI, utilice la sintaxis siguiente:
  
  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1
  
  ```
