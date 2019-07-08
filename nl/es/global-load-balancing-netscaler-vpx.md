---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: load balancing, vpx, global, mep, gslb

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Equilibrio de carga global con Citrix NetScaler VPX
{: #global-load-balancing-with-citrix-netscaler-vpx}

El equilibrio de carga de servidor global (GSLB) es un mecanismo para distribuir el tráfico entre diversos servidores/instancias que normalmente se encuentran en diferentes ubicaciones geográficas. La idea es tener un servidor/motor de equilibrio global que reciba solicitudes de tráfico y las redireccione a ciertas ubicaciones, utilizando los criterios/algoritmos seleccionados y configurados por el administrador. Para ello, se pueden utilizar dos métodos reconocidos dentro de la red de {{site.data.keyword.BluSoftlayer_notm}}:

* **CDN:** Red de entrega de contenido (CDN) emitida para entregar contenido y medios enriquecidos como imágenes y videos, la CDN distribuye contenido en nodos geográficamente dispersos, manteniendo la menor latencia y las velocidades más altas. Normalmente se implementa cuando se deben distribuir partes particulares de contenido en lugar de sitios web y aplicaciones enteras. {{site.data.keyword.BluSoftlayer_notm}} ofrece este servicio, lea más al respecto [aquí](/docs/infrastructure/CDN?topic=CDN-getting-started).
* **NetScaler VPX:** Al igual que con el equilibrio de carga local normal, VPX utiliza una jerarquía de objetos similar para equilibrar la carga de tráfico entre varias geografías. Utilizando búsquedas globales basadas en DNS, NetScaler elige el registro respectivo que corresponde a la ubicación/sitio seleccionado, la selección se basa en los criterios preconfigurados por el administrador. Las siguientes secciones ampliarán la información sobre esta opción/oferta.

Hay otras técnicas disponibles para la distribución de contenido, como por ejemplo la redirección HTTP, que también puede aplicarse con Citrix NetScaler VPX.
{: note}

## Acerca del GSLB en VPX
{: #about-gslb-on-vpx}

NetScaler VPX puede habilitarse con GSLB activando su característica en la CLI/GUI.

GSLB utiliza componentes/objetos muy similares a los utilizados en los despliegues de equilibrio de carga locales, donde las entidades se definen utilizando un modelo jerárquico.

GSLB puede aplicarse para varios propósitos. Algunos de ellos son:

* **Compartición/distribución de cargas:** Para distribuir los recursos de forma eficiente e inteligente entre varias ubicaciones.
* **Recuperación tras desastre:** Se utiliza cuando la ubicación principal o primaria se apaga o no puede representar el servicio. En este caso de ejemplo se puede presuponer una ubicación alternativa/copia.
* **Rendimiento/remodelado:** Le permite colocar contenido más cerca de los sistemas, o en una forma que mejore el servicio en cuestión.

Los principales componentes o entidades en el proceso/despliegue de GSLB son:

* **Servidores virtuales:**: Una VIP es una dirección IP a la que los clientes envían solicitudes, NetScaler finaliza la conexión del cliente en la VIP y luego inicia una conexión con un servidor configurado en el servicio de equilibrio de carga.
* **DNS (Sistema de nombres de dominio) y servidores de nombres:** La resolución de nombres en GSLB funciona de forma muy parecida que el DNS normal. La diferencia es la lógica/criterios utilizados para determinar las direcciones resueltas, GSLB utiliza un método de equilibrio de carga preconfigurado para manejar esta resolución. NetScaler puede configurarse para interactuar con el DNS de diferentes maneras:
	* DNS autorizado (ADNS). Los NetScalers que utilizan el modo ADNS están autorizados para un dominio particular y todos sus registros.
	* Subdelegación de DNS. Se produce cuando un servidor DNS (autorizado del dominio) delega la responsabilidad de un subdominio a un sistema NetScaler.
	* Proxy de DNS. Cuando se configura en esta modalidad, NetScalers reenvía las solicitudes DNS a otro servidor (externo) manejando la resolución de nombre.
* **Método:** El método es un algoritmo que utiliza el servidor virtual GSLB para seleccionar el mejor servicio de GSLB de la topología. El algoritmo evalúa aspectos de rendimiento que corresponden a los criterios de selección real. Están disponibles los métodos siguientes:
  * Round Robin: Alterna las solicitudes entrantes para que se manejen entre sitios o servicios de GSLB independientemente de su carga.
  * Tiempo de ida y vuelta (RTT): Una medida de tiempo o retraso entre el servidor DNS local del cliente y los sitios (GSLB). NetScaler utiliza diferentes mecanismos como la solicitud de eco/respuesta ICMP (PING), UDP y TCP, para recopilar métricas de RTT.
  * Proximidad estática: Utiliza una base de datos de direcciones IP para establecer la proximidad entre el servidor DNS local del cliente y los sitios y luego la utiliza como criterio para hacer una selección.
  * Conexiones mínimas: Mide el menor número de conexiones activas en cada sitio/servicio como criterio de selección.
  * Tiempo de respuesta mínimo: Selecciona el sitio con el menor número de conexiones activas y el tiempo de respuesta promedio más bajo.
  * Ancho de banda mínimo: Elige el sitio que gestiona actualmente la menor cantidad de tráfico (Mbps).
  * Menos paquetes: Selecciona el servicio que ha recibido menos paquetes en los últimos 14 segundos.
  * Hash de dirección IP origen: Realiza una selección de servicio basada en el valor de hash de las direcciones IPv4 o IPv6 del cliente.
  * Carga personalizada: Selecciona un servicio que no está gestionando ninguna transacción activa. Si todos los servicios en la configuración de equilibrio de carga están manejando transacciones activas, el dispositivo selecciona el servicio con la menor carga (uso de CPU, memoria y tiempo de respuesta).

* **MEP (Metric Exchange Protocol):** Un protocolo de propiedad utilizado para intercambiar métricas (de carga y de red) e información de persistencia entre sitios. El MEP proporciona una comprobación de estado entre los diferentes sitios/NetScalers en la topología/malla de GSLB. Utilizando los criterios establecidos por el administrador, el MEP proporciona una forma para que los sitios se comuniquen y manejen el tráfico basándose en los parámetros de selección configurados anteriormente. El MEP utiliza los puertos TCP 3009 y 3011. Cuando el MEP está inhabilitado, la selección de métodos se limita a las opciones listadas anteriormente, marcadas con un asterisco (*). Cualquier otro método elegido se revertirá en Round Robin.
* **Supervisión:** El motor de NetScaler evalúa periódicamente el estado de los servicios remotos de GSLB mediante el MEP o una supervisión explícita limitada a los servicios en cuestión. Los supervisores se utilizan como en un servicio de equilibrio de carga normal. En el caso del GSLB, no es necesario añadir supervisores a los servicios locales ya que está normalmente controlado por el MEP.
* **Persistencia:** Una característica opcional que establece una preferencia de sitio para un dominio concreto. En este caso de uso concreto, el centro de datos no equilibra la carga del tráfico pero sí lo maneja. Esto puede ser útil en determinadas aplicaciones, como el comercio electrónico, donde los datos transaccionales son exclusivos para cada sitio/servidor.
* **Sitio de GSLB:** Los sitios se pueden definir como centros de datos o ubicaciones donde un sistema de NetScaler está configurado/presente. Cada sitio de GSLB lo gestiona un sistema de NetScaler que se considera "local" en ese sitio, mientras que todos los demás sistemas/sitios remotos son vistos y tratados como sitios "remotos".
* **Servicio de GSLB:** Es un objeto que representa (y está limitado a) un servidor virtual/VIP normal. Puede ser local (mismo sitio) o remoto.
* **Servidor virtual de GSLB:** Un servidor virtual de GSLB se asigna a uno o varios servicios de GSLB que normalmente son parte de diferentes sitios (GSLB). El tráfico recibido obtiene la carga equilibrada entre los sitios enlazados. La selección sitio se realiza basándose en el método y el caso de uso.
* **Dominio de GSLB:** Representa el dominio o zona de la que es responsable el servidor virtual de GSLB.
* **Servicio de ADNS:** Un servicio representado por una combinación de dirección IP y puerto, donde se envían las solicitudes de DNS a un dominio en el que está autorizado un NetScaler. NetScaler toma los servidores virtuales de GSLB enlazados a ese dominio para obtener una respuesta.
