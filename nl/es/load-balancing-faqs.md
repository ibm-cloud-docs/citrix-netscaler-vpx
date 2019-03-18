---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}

# Preguntas más frecuentes de Citrix NetScaler VPX
{: #faqs-for-citrix-netscaler-vpx}

Las siguientes son las preguntas más frecuentes relacionadas con Citrix NetScaler VPX.

## ¿Qué es Citrix NetScaler VPX?
{:faq}

Citrix NetScaler es un controlador de entrega de aplicaciones que hace que las aplicaciones sean hasta cinco veces mejor acelerando el rendimiento, garantizando la disponibilidad y seguridad de la aplicación y disminuyendo sustancialmente los costes operativos. Elija la edición de Citrix NetScaler que mejor cumpla los requisitos de su aplicación y despliéguela en el sistema dedicado adecuado para sus necesidades de rendimiento. Para obtener más información sobre Citrix NetScaler, consulte la [página de NetScaler ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){:new_window} en el sitio web de Citrix.

## ¿Por qué es necesario el equilibrio de carga?
{:faq}

El equilibrio de carga de tráfico se ha convertido en un aspecto clave de muchas implementaciones de clientes ya que distribuye las solicitudes y cargas de aplicaciones en varios servidores. También proporciona una serie de ventajas para la topología general, incluidas:

* Seguridad. Se crea un aislamiento lógico de los servidores de aplicaciones o se deniegan solicitudes de tráfico en función de los protocolos de IP y números de puerto.
* Alta disponibilidad. El contenido se replica en una agrupación o grupo de servidores, para garantizar su disponibilidad para los hosts.
* Escalabilidad. Se pueden añadir servidores adicionales a medida que aumenta la demanda, permitiendo al equilibrador de carga distribuir la carga de trabajo en los servidores adicionales.
* Eficacia. Las cargas de trabajo se distribuyen dinámicamente cuando se configura el equilibrio de carga. Por ejemplo, los recursos como CPU se pueden utilizar de forma más eficiente.

## ¿Cuántas opciones de equilibrio de carga hay disponibles en {{site.data.keyword.BluSoftlayer_notm}}?
{:faq}

Para obtener una comparación detallada de las ofertas de equilibradores de carga de IBM©, consulte [Explorar los equilibradores de carga](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore).

## ¿NetScaler soporta IPv6?
{:faq}

Sí. Tanto IPv6 como IPv4 están soportados en la red pública de {{site.data.keyword.BluSoftlayer_notm}}.

## ¿NetScaler equilibra la carga de tráfico en la red privada?
{:faq}

Sí, NetScaler es el único producto de equilibrio de carga de {{site.data.keyword.BluSoftlayer_notm}} que se amplía en la red privada.

## ¿Puede configurarse NetScaler para informar de la dirección IP de origen del cliente en lugar de la dirección IP de origen del dispositivo NetScaler?
{:faq}

Sí, el parámetro **Utilizar IP de (USIP)** puede establecerse en **SI** en la interfaz de gestión avanzada de NetScaler para permitir los informes de IP de origen del cliente en lugar de la IP de NetScaler.

Habilitando la modalidad de dirección USIP en el dispositivo se añade flexibilidad al dispositivo para utilizar la dirección IP del cliente, disponible en la cabecera de IP, cuando se comunica con el servidor. Habilitando este modo, el dispositivo abre conexiones de servidor con la dirección IP del cliente y también factoriza la dirección IP del cliente en la reutilización de conexiones. Por lo tanto, este modo facilita la reutilización limitada por cliente basándose en la dirección IP del cliente.

## ¿Cuáles son los distintos puertos utilizados para intercambiar información relacionada con la alta disponibilidad entre los nodos en una configuración de alta disponibilidad?
{:faq}

El puerto 3010, para la propagación de mandatos y la sincronización. El puerto UDP 3003, para intercambiar paquetes de señales de latido.

## ¿Qué versión de NetScaler VPX incluye el equilibrio de carga del servidor global (GSLB)?
{:faq}

Platino.

## ¿Puedo tener NetScaler en la configuración de alta disponibilidad?
{:faq}

Sí, los dispositivos NetScaler VPX soportan las configuraciones de alta disponibilidad (HA).

Los servidores de NetScaler VPX no son servidores redundantes, a menos que se configure en modo HA con un socio. Como parte de la estrategia de copia de seguridad y recuperación, es muy recomendable desplegar un entorno de alta disponibilidad cuando se utiliza NetScaler VPX.

También es importante proporcionar redundancia para otros componentes de hardware y software. Por ejemplo, las fuentes de alimentación y las unidades de disco local no tienen redundancia. Un fallo en estos componentes puede provocar la pérdida de datos.

## ¿La oferta de NetScaler de {{site.data.keyword.BluSoftlayer_notm}} incluye la funcionalidad de VPN con SSL?
{:faq}

Sí, esta característica se conoce como NetScaler Gateway™ y está incluida en todas las ediciones.  Para obtener más información sobre esta característica, visite el [sitio de Citrix ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.citrix.com/products/netscaler-adc/){: new_window}
