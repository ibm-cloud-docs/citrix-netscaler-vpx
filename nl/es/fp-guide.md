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

# Configuración de la redirección de tráfico de proxy directo utilizando el dispositivo Citrix NetScaler VPX
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

Esta guía le proporciona la configuración paso a paso de una configuración de proxy directo mediante el dispositivo Citrix NetScaler VPX. Se ha realizado una prueba de esta configuración en un dispositivo Citrix NetScaler VPX que ejecuta una versión de software 11.1 (edición platino) y tiene un rendimiento de 10Mbps.

<img src="images/fp1.png" alt="dibujo" style="width: 600px;"/>

## Qué conseguirá

En esta guía paso a paso aprenderá cómo configurar el servicio:

Tarea  | Descripción
------------- | -------------
[Solicitar Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) | Empezar solicitando un dispositivo Citrix NetScaler VPX.
[Solicitar una subred privada](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) | Solicitar una subred privada del soporte de IBM© para su cuenta.
[Habilitar la redirección de la memoria caché y las prestaciones de equilibrio de carga](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) | Identificar los recursos de la aplicación como, por ejemplo, las agrupaciones de origen y los mecanismos de comprobación de estado.
[Configurar el servidor virtual de DNS](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) | Añadir los servicios de resolución de DNS, definir el grupo de servicios de DNS y definir el servidor virtual de DNS.
[Configurar la redirección de memoria caché para el tráfico HTTP(S)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-s-traffic) | Configurar la redirección de memoria caché para el servidor virtual de proxy directo con el tráfico HTTP o HTTPS.
[Configurar la redirección de memoria caché para el tráfico SSL (opcional)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) | Configurar la redirección de memoria caché para su servidor virtual de proxy directo con tráfico SSL en lugar de HTTP o HTTPS.
[Configurar la conversión de direcciones de red de origen para el tráfico de salida](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) | Utilice el dispositivo Citrix NetScaler VPX para realizar la conversión de direcciones de red en el tráfico de salida desde las máquinas cliente.
[Actualizar los valores de proxy en el navegador de Internet de la máquina cliente (opcional)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) | Actualizar los valores de proxy utilizando el navegador de Internet de la máquina cliente, si lo desea.
