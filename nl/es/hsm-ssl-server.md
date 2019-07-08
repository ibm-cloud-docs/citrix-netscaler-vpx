---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, security, add, configure

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

# Añadir y configurar el servidor virtual SSL
{: #add-and-configure-the-ssl-virtual-server}

Para añadir y configurar el servidor virtual SSL, realice el procedimiento siguiente:

1. Vaya a **Sistema > Valores > Configurar características básicas**. Seleccione **Descarga SSL** y pulse **Aceptar**.
2. En la GUI de Netscaler, vaya a **Gestión de tráfico > Equilibrio de carga > Servicios > Añadir** y especifique el nombre, la dirección IP y establezca el protocolo como **HTTP**. Pulse **Aceptar** para finalizar.
3. Confirme que el servicio está operativo:

	<img src="images/15-confirm-service.png" alt="dibujo" style="width: 700px;"/>

4. Repita el paso dos para cualquier servidor adicional.
5. Vaya a **Gestión de tráfico > Equilibrio de carga > Servidores virtuales >** y pulse **Añadir**. Especifique el nombre y seleccione **SSL** como protocolo y, a continuación, especifique la dirección IP pública. Pulse **Aceptar** para finalizar.
6. Ahora seleccione **Sin enlace de servicio de servidor virtual de equilibrio de carga** y pulse **Seleccionar**. Elija los servicios que ha creado en los pasos anteriores y pulse Seleccionar y, a continuación, pulse **Enlazar/Continuar**.

	<img src="images/18-bind-service.png" alt="dibujo" style="width: 700px;"/>

7. Por último, pulse **Ningún certificado de servidor**, a continuación, pulse **Seleccionar certificado de servidor** y seleccione el certificado que ha instalado anteriormente. Pulse **Seleccionar**, luego **Enlazar/Continuar** y **LISTO** para finalizar.
