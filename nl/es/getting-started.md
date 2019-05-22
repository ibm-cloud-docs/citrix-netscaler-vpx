---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación al dispositivo de software de Citrix NetScaler VPX
{: #getting-started}

El despliegue de Citrix NetScaler VPX en la solución de {{site.data.keyword.BluSoftlayer_notm}} acelera la entrega de aplicaciones web, mejora el rendimiento y garantiza que sus aplicaciones y servicios en la nube están optimizados, disponibles y seguros. Si tiene cargas de trabajo difíciles, como por ejemplo juegos, Big Data y análisis, o nubes privadas, Citrix NetScaler VPX puede ayudarle a ofrecer su solución cuando, donde y cómo los usuarios más lo necesiten.

## Antes de empezar
Para empezar con Citrix NetScaler VPX, necesitará conocer la siguiente información:

* La información de inicio de sesión del Portal de clientes de IBM© Cloud
* La ubicación de despliegue para el equilibrador de carga
* Qué tipo de Netscaler se ajusta mejor a sus necesidades (para obtener más información, consulte [Explorar los equilibradores de carga](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore))
* El número de direcciones IP públicas necesarias
* La VLAN donde desea asignar el equilibrador de carga

## Solicitud de un Citrix NetScaler VPX

Para solicitar un dispositivo de software Citrix NetScaler VPX, vaya a la página de pedido en el Portal de clientes:

1. En el navegador, abra el [Portal de clientes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window} e inicie sesión en su cuenta.
2. En la navegación del Portal de clientes, seleccione **Dispositivos > Lista de dispositivos** y pulse el enlace **Pedir dispositivos**.
3. En la página **Pedir servicios y productos de SoftLayer** desplácese hasta la sección Red y pulse el enlace **Pedido** en Citrix NetScaler VPX.
4. Seleccione una ubicación en el menú desplegable donde desee desplegar su dispositivo de software de Citrix NetScaler VPX.  
5. Seleccione el mejor tipo de NetScaler para su edición de software, versión de software y las necesidades de rendimiento.
6. Seleccione el número de las direcciones IP públicas que necesite.  
	Son las direcciones IP públicas estáticas, desplegadas como direcciones IP virtuales (VIP) en el NetScaler VPX.
7. Pulse **Continuar**.
8. Especifique la información requerida por ARIN (o la organización equivalente en su región de despliegue) para las direcciones IP que ha solicitado.
9. Especifique la información de contacto.
10. Seleccione su VLAN.
	Para minimizar la latencia y garantizar la utilización optimizada de los recursos de red, asigne el Citrix NetScaler VPX a la misma VLAN que los servidores donde se distribuirá el tráfico.
11. Revise el pedido, acepte los términos y pulse **Realizar pedidos**. El dispositivo de software de Citrix NetScaler VPX se despliega con los valores seleccionados.

## Qué hacer a continuación

Encontrará más información sobre las [características](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-about-citrix-netscaler-vpx) de Citrix Netscaler VPX, revisar [terminología](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-citrix-netscaler-vpx-terminology) específica de Netscaler, o empezar a [configurar](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-basic-load-balancing-configuration) Netscaler.
