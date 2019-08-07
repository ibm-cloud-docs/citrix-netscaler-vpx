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

# Configuración de VPN de sitio a sitio de IPSec en {{site.data.keyword.vpx_full}} con IBM Virtual Router Appliance
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

En esta guía se proporcionan instrucciones paso a paso para configurar una conexión IPSec VPN de sitio a sitio en Citrix VPX. Se utiliza un IBM Virtual Router Appliance (VRA) como homólogo de VPN.

<img src="images/ipsec1.png" alt="dibujo" style="width: 600px;"/>

## Acerca del despliegue
El despliegue se ha creado y probado con las especificaciones de componente siguientes:

| Versión y compilación de NetScaler VPX	| Versión y Descripción de VRA | 
| ------------- | ------------- | 
| NS12.1: compilación 48.13.nc | AT&T vRouter 5600 1801q |

Necesita una licencia Platinum de VPX para configurar una VPN de IPSec.
{: note}

## Antes de empezar

Esta guía presupone que es propietario de los dos dispositivos. Visite los enlaces siguientes para hacer un pedido.

-	[Iniciación al dispositivo de software de {{site.data.keyword.vpx_full}}](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[Iniciación a IBM Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## Qué conseguirá

En esta guía aprenderá a configurar una VPN de IPSec en un dispositivo Citrix VPX.

Tarea  | Descripción
------------- | -------------
[Habilitar las características obligatorias en VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) | Primero, debe habilitar las características necesarias para crear la VPN de IPSec.
[Crear un perfil de IPSec](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile) | El perfil de IPSec incluye los parámetros de seguridad para establecer la conexión. 
[Crear un túnel de IP](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) | En esta sección, crearemos un objeto de túnel de IP para especificar direcciones IP locales y remotas, así como los parámetros de protocolo.
[Crear un direccionamiento basado en políticas (PBR- Policy Based Routing)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing) | Se utiliza PBR para definir los parámetros de tráfico exclusivos para las subredes tanto locales como remotas.
[Configurar VRA](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra) | Configure Virtual Router Appliance, utilizando sintaxis de configuración de VPN equivalente.
[Verificar el estado de la VPN](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection) | Verifique el estado de funcionamiento de la VPN y lleve a cabo una sencilla prueba de conectividad.

## Recursos adicionales
Los siguientes recursos adicionales le permitirán aprender más sobre Citrix VPX y Virtual Router Appliance.

* [CloudBridge Connector ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configuración de un túnel de CloudBridge Connector entre un dispositivo Citrix ADC y el dispositivo iOS de Cisco ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Documentación de Citrix VPX/ADC 12.1 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [Documentación adicional de VRA](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
