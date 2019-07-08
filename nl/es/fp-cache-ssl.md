---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, redirect, ssl, traffic

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

# Configurar la redirección de memoria caché para el tráfico SSL (opcional)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

En lugar de definir la redirección del servidor virtual con un protocolo HTTP o HTTPS (tal como se describe en el paso anterior), es posible que desee definirlo para manejar el tráfico SSL.

Para ello, siga estos pasos:

1. Vaya a **Gestión de tráfico > Redirección de memoria caché > Servidores virtuales** y pulse **Añadir**. Especifique el nombre de su servidor virtual proxy directo, seleccione el protocolo SSL y un tipo de memoria caché de **REENVÍO**. Asígnele una dirección IP de la subred privada con su puerto de requisito.

	<img src="images/fp14.png" alt="dibujo" style="width: 300px;"/>

	Pulse **Aceptar**.

2. Revise la página de resume y pulse **Aceptar** para continuar.
3. Especifique las configuraciones de Redirección, Servidor virtual DNS y Servidor virtual de destino.
4. Pulse **Certificado** en el panel **Configuración avanzada** para ver la configuración relacionada con el certificado SSL.
5. Pulse el campo vacío **Ningún certificado de servidor**.
6. En la lista desplegable Seleccionar certificado de servidor, seleccione el servidor SSL.
7. Especifique la información de configuración del certificado según sea necesario.

	<img src="images/fp15.png" alt="dibujo" style="width: 400px;"/>

	Pulse **Instalar**.

8. Seleccione **Enlazar**.

	<img src="images/fp16.png" alt="dibujo" style="width: 300px;"/>
