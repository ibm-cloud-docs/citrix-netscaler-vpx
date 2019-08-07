---

copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: dns, cache, virtual server

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

# Configurar el servidor virtual de DNS
{: #configure-the-dns-virtual-server}

Para configurar el servidor virtual de DNS:

1. Vaya a Gestión de tráfico > Equilibrio de carga > Servidores.
2. Pulse Añadir para añadir dos servicios de resolución de DNS de IBM© SoftLayer - 10.0.80.11 y 10.0.80.12.

	<img src="images/fp5.png" alt="dibujo" style="width: 200px;"/> <img src="images/fp5b.png" alt="dibujo" style="width: 200px;"/>

3. A continuación, cree y defina un Grupo de servicios de DNS; para ello vaya a Gestión de tráfico > Equilibrio de carga > Grupos de servicios y seleccione Añadir.

	<img src="images/fp6.png" alt="dibujo" style="width: 400px;"/>

4. Seleccione el protocolo DNS y pulse Aceptar.

	<img src="images/fp7.png" alt="dibujo" style="width: 300px;"/>

5. En la pantalla siguiente, añada los servicios de resolución de DNS a este grupo de servicio de DNS pulsando primero el campo vacío en **Miembros del grupo de servicios**.

6. En el panel Crear miembro de grupo de servicios, especifique el puerto 53 de DNS y pulse Crear.

	<img src="images/fp8.png" alt="dibujo" style="width: 200px;"/>

7. Pulse Cerrar y, a continuación, Terminado.

	Suponiendo que los dos servicios de resolución de DNS de IBM Softlayer se pueden obtener en el dispositivo {{site.data.keyword.vpx_full}}, el grupo de servicios se mostrará en verde.

8. Vaya a Gestión de tráfico > Equilibrio de carga > Servidores virtuales y pulse Añadir para definir el servidor virtual de DNS.
9. En Valores básicos, asigne un nombre al servidor virtual, elija el puerto 53 y el protocolo de DNS y asigne una dirección IP de la subred privada.

	<img src="images/fp9.png" alt="dibujo" style="width: 300px;"/>

10. En la página siguiente, pulse en el campo vacío con la etiqueta **Ningún enlace de ServiceGroup del servidor virtual de equilibro de carga**.
11. Seleccione el grupo de servicio de DNS definido anteriormente en la lista desplegable y pulse Enlazar.  

	<img src="images/fp10.png" alt="dibujo" style="width: 300px;"/>

12. Pulse en Continuar y, a continuación, Terminado.

El estado del servidor virtual de DNS debería mostrarse en verde.

<img src="images/fp11.png" alt="dibujo" style="width: 500px;"/>
