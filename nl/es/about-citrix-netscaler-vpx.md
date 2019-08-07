---

copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: about, vpx, features, overview

subcollection: citrix-netscaler-vpx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Acerca de {{site.data.keyword.vpx_full}}
{: #about-citrix-netscaler-vpx}

El {{site.data.keyword.vpx_full}} es un dispositivo de software virtual dedicado que proporciona equilibrio de carga tanto en la red de IBM© Cloud pública como en la privada.

El despliegue de {{site.data.keyword.vpx_full}} en la solución de {{site.data.keyword.BluSoftlayer_notm}} acelera la entrega de aplicaciones web, mejora el rendimiento y garantiza que sus aplicaciones y servicios en la nube están optimizados, disponibles y seguros. Si tiene cargas de trabajo difíciles, como por ejemplo juegos, Big Data y análisis, o nubes privadas, {{site.data.keyword.vpx_full}} puede ayudarle a ofrecer su solución cuando, donde y cómo los usuarios más lo necesiten.

## Características
{: #features}

* El único producto que puede equilibrar la carga del tráfico en redes públicas y privadas
* Gestión utilizando la GUI (interfaz gráfica de usuario) o la CLI (interfaz de línea de mandatos)
* Muchos tipos de distribución del tráfico, incluyendo:
  * Conexiones mínimas
  * Round Robin
  * Tiempo de respuesta mínimo
  * Ancho de banda mínimo
  * Paquetes mínimos
  * Hash de URL
  * Hash de nombre de dominio
  * Hash de dirección IP de origen
  * Hash de dirección IP de destino
  * IP de origen - Hash de IP de destino
  * Señal
  * LRTM

* Aceleración SSL / descarga SSL
* GSLB (equilibrio de carga de servidor global)
  * Utiliza la infraestructura de DNS para conectar el cliente al mejor centro de datos
  * Supervisa la carga y la disponibilidad de centros de datos para seleccionar las mejores opciones de conexión
* Cambio de contenido
* Redirección de memoria caché
* Capacidades de cortafuegos de aplicaciones
* Características de seguridad de aplicaciones
* Dispositivo virtual en ejecución en hardware dedicado
* Despliegue como cualquier otro servidor de {{site.data.keyword.BluSoftlayer_notm}}, con la flexibilidad y disponibilidad en mente
* Ofrecido en los niveles de ancho de banda: 10Mbps, 200Mbps y 1000Mbps

El {{site.data.keyword.vpx_full}} puede desplegarse a petición, en tan solo 15 minutos, en cualquier centro de datos de {{site.data.keyword.BluSoftlayer_notm}} en todo el mundo. Varios modelos de licencia incluyen la velocidad y las características que necesita y ofrecen la flexibilidad que exigen las soluciones de nube actuales. Esta flexibilidad garantiza un buen ajuste para cada caso de uso, desde implementaciones medianas hasta las grandes empresas.

{{site.data.keyword.BluSoftlayer_notm}} ofrece el dispositivo virtual NetScaler VPX con acceso raíz completo sin restricciones.   

## Seguridad de aplicación
{: #application-security}

Para proteger el tráfico de la aplicación, los clientes pueden aprovechar las características de seguridad como el filtro de contenido de aplicación y un cortafuegos de aplicación web.

## Filtrado del tráfico
{: #traffic-filtering}

El {{site.data.keyword.vpx_full}} filtra las solicitudes de los usuarios a los servidores y las respuestas de los servidores a los usuarios. Una característica de aprendizaje con el cortafuegos de aplicaciones permite el establecimiento de perfiles de sesiones en tiempo real y la determinación de si se permite el tráfico.

## Informes PCI-DSS
{: #pci-dss-reporting}

Los estándares de seguridad de datos de Payment Card Industry (PCI) consisten en doce criterios que deben cumplir las empresas que procesan pagos con tarjeta de crédito en línea. Los informes PCI-DSS constan de una lista de los criterios que son relevantes para la configuración del cortafuegos de su aplicación. El informe también muestra si la configuración actual cumple con cada criterio y sugiere cómo configurar el cortafuegos de aplicaciones para satisfacer esos estándares.

## Equilibrio de carga global (GSLB)
{: #global-load-balancing-gslb-}

La edición platino del NetScaler amplía el equilibrador de carga más allá de los límites locales del centro con la funcionalidad de equilibrio de carga global.

## Ampliar el centro de datos
{: #extend-your-datacenter}

NetScaler Platinum Edition le permite utilizar la característica NetScaler CloudBridge Connector, que proporciona una forma sencilla de ampliar el centro de datos a {{site.data.keyword.BluSoftlayer_notm}} con menús controlados por el asistente.
