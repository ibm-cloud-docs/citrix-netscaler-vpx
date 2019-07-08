---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: default, deployment, configure, configuration

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Despliegue predeterminado de Citrix NetScaler VPX
{: #citrix-netscaler-vpx-default-deployment}

Cuando echa un vistazo a su NetScaler en **Dispositivos > Lista de dispositivos** en el [Portal de clientes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/) es posible que vea que es diferente a los otros servidores. Concretamente, el dispositivo tiene una dirección IP privada pero no una dirección IP pública.

El despliegue predeterminado de un NetScaler en {{site.data.keyword.BluSoftlayer_notm}} está diseñado para ser lo más seguro posible, asignando automáticamente una dirección IP privada como IP de NetScaler (NSIP) utilizada para fines de gestión. Si pulsa la flecha a la izquierda del NetScaler, la línea se expande para mostrar el nombre de usuario predeterminado (root) y la contraseña de usuario root enmascarada.

{{site.data.keyword.BluSoftlayer_notm}} maneja muchas de las decisiones por usted durante el suministro. Por ejemplo, qué direcciones IP utilizar para qué fines. Le pregunta qué VLAN desea utilizar para el despliegue. También, automatiza gran parte de la configuración back-end utilizando scripts y una API, como por ejemplo la asignación de interfaces para separar las VLAN públicas y privadas y asignar las direcciones IP adecuadas a cada interfaz, incluyendo las NSIP, VIP y SNIP.

## ¿Qué debo configurar?
{: #what-do-i-need-to-configure-}

De forma predeterminada, la NSIP es la dirección IP privada asignada durante el suministro, que es la dirección IP que utiliza para conectarse al NetScaler para fines de gestión. Las SNIP (direcciones IP de la subred), de forma predeterminada, se asignan desde las mismas subredes de IP primaria que se encuentran en la VLAN que ha elegido durante el proceso de pedido.

Si elige la misma VLAN en la que residen los servidores de carga equilibrada, no es necesaria una configuración adicional de estas SNIP. De forma predeterminada, el DNS se establece en el servidor de nombres de {{site.data.keyword.BluSoftlayer_notm}}. En una implementación básica, si {{site.data.keyword.BluSoftlayer_notm}} aloja los registros DNS para los servidores, entonces no es necesaria ninguna configuración adicional.
