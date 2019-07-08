---

copyright:
  years: 2019
lastupdated: "2019-04-28"

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

# Crear un direccionamiento basado en políticas (PBR - Policy Based Routing)
{: #creating-policy-based-routing}

Se necesita una política de direccionamiento basado en políticas (PBR) para especificar los parámetros de tráfico exclusivos (como por ejemplo subredes locales y remotas) que utilizará la conexión VPN. Para crear un perfil de PBR efectúe los pasos siguientes:

1.	Vaya a **Sistema > Red > PBR** y seleccione **Añadir**.
2.	Especifique **Nombre**.
3.	Deje **Acción** con su valor predeterminado **ALLOW**.
4.	En **Siguiente tipo de salto**, seleccione **túnel de IP**, y seleccione un túnel [creado anteriormente](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) en la lista desplegable **Nombre de túnel de IP**.
5.	Asegúrese de seleccionar **Habilitar PBR**.
6.	En la sección **Configurar IP**, seleccione **=** en el campo **Operación** tanto para origen como para destino.
7.	Especifique la primera y la última IP de subred en los campos siguientes:
  *	**IP de origen baja**
  *	**IP de origen alta**
  *	**IP de destino baja**
  *	**IP de destino alta**
8.	Pulse **Crear**.

    <img src="images/ipseCreatePBR1.png" alt="dibujo" style="width: 200px;"/>

9.	En **Sistema > Red > PBRs**, seleccione la nueva PBR, pulse en la lista **Seleccionar acción** y pulse **Aplicar**.

    <img src="images/ipsecCreatePBR2.png" alt="dibujo" style="width: 600px;"/>

Para crear el perfil de PBR en la CLI, utilice la sintaxis siguiente:

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs
  
  ```
  {: codeblock}

  Sepa que cualquier instancia de servidor virtual o infraestructura que tenga que pasar por el túnel VPN y quedarse tras la VPX, se tendrá que configurar para utilizar VPX como pasarela predeterminada o para utilizar una ruta estática. Esto enviará el tráfico a la VPX cuando el destino sea la subred remota (homóloga). Vea el siguiente ejemplo de ruta estática (**10.115.0.0/16**).
  {: note}

  ```
  >route print
  ===========================================================================
  Interface List
  3...06 93 7a 03 f0 b3 ......XenServer PV Network Device #0
  4...06 ff 8f 6d 89 e8 ......XenServer PV Network Device #1
  1...........................Software Loopback Interface 1
  7...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
  10...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
  ===========================================================================
  
  IPv4 Route Table
  ===========================================================================
  Active Routes:
  Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0    169.54.255.65    169.54.255.73     26
       10.115.0.0      255.255.0.0      192.168.0.1      192.168.0.2     26
  
  ```
  {: codeblock}
