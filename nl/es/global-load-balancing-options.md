---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Equilibrio de carga global

El equilibrio de carga de servidor global (GSLB) es un método para dividir el tráfico en varios servidores utilizando DNS y ubicaciones geográficas como medio para determinar dónde se debe enviar el tráfico. Generalmente, un equilibrador de carga global envía una solicitud de cliente a un servidor cercano al cliente, disminuyendo la latencia y mejorando el rendimiento.

Puede que no necesite una implementación completa de una solución de equilibrio de carga global. GSLB requiere varias instancias de un dispositivo adecuado que pueda realizar esta función y, dependiendo de sus necesidades, es posible que otras soluciones le sean más atractivas. Si necesita sitios web y aplicaciones completas, GSLB es una buena opción. Si solo necesita partes de su contenido, como imágenes, vídeos u otros archivos grandes, es posible que la [Red de entrega de contenido](https://console.bluemix.net/docs/infrastructure/CDN/about.html#about-content-delivery-networks-cdn-){: new_window} sea más adecuada (y más fácil de desplegar).

## Citrix NetScaler VPX

Citrix NetScaler VPX es el único dispositivo configurable por el cliente que realiza un equilibrio de carga global verdadero. NetScaler es un dispositivo multifunción que puede realizar búsquedas de equilibrio de carga global basadas en DNS. Puede apuntar a NetScaler como servidor DNS y el dispositivo buscará el equilibrio de carga en los servidores en que está configurado, realizará un cálculo de distancia y devolverá un registro con la IP del servidor más cercano a la solicitud del cliente.

Para el equilibrio de carga global, tendría una configuración de dispositivo de NetScaler en cada centro de datos. Cada configuración de dispositivo de NetScaler puede ser un Netscaler único o un par de Netscalers en un par de HA, dependiendo de sus requisitos, proporcionando servicios de equilibrio de carga local para los servidores tras ellos. Los dispositivos están configurados para comunicarse entre ellos para que puedan intercambiar información de estado en cada servidor asignado a la rotación de equilibrador de carga global. Cualquier solicitud de DNS que llega a estos NetScalers configurados puede devolver un registro apropiado para un servidor que esté en línea y respondiendo. Cualquier servidor que no responda se elimina de la rotación y se selecciona otro.

Debe tener configurado el equilibrio de carga incluso aunque solo se equilibre un servidor. Necesitará direcciones IP adicionales para algunos servicios, a saber, la IP del sitio del GSLB. Esta IP la utiliza NetScaler para comunicarse con los otros NetScalers en el protocolo de equilibrio de carga global. 

El siguiente procedimiento de equilibrio global utiliza:

### VPX1

`50.97.235.236` se denomina `VPX1Vserver` y es la VIP del equilibrio de carga local para ese dispositivo. `50.23.66.52` se denominará `VPX1site` y es la IP local para el GSLB de ese dispositivo.

### VPX2
`208.43.241.249` se utiliza para `VPX2Vserver` y la IP del GSLB es `208.43.224.4`, denominada `VPX2site`.

1. Vaya a **Gestión de tráfico > GSLB** y pulse el botón derecho para habilitar la característica. A continuación, seleccione **Sitios** y **Añadir**.

2. En el primer dispositivo, introduzca el nombre VPX1, el tipo Local y la IP `50.23.66.52` y seleccione **Cerrar**. 

	Verá el sitio listado con un estado en verde. No añada todavía un sitio remoto.

3. Vaya a **Gestión de tráfico > GSLB** y seleccione el **Asistente de GSLB**. Pulse **Siguiente**. Introduzca el nombre de host para el que equilibrará la carga (en este ejemplo: `gslb.tsstesting.com`), deje el tipo de registro A y el tipo de servicio Cualquiera. El nombre del servidor virtual se completará solo. Pulse **Siguiente**.

4. Elija su formulario de equilibrio y método de persistencia del mismo modo que haría con un equilibrio de carga normal. Pulse **Siguiente**.

5. El sitio ya está completo así que no debe añadir nada. En su lugar, pulse el '+' verde junto al nombre del primer sitio. Seleccione el servidor virtual en ese dispositivo desde la lista y pulse **Crear**. Debería ver que el sitio está configurado con la IP de sitio y la IP del servidor virtual de su configuración de equilibrio de carga y que es verde. Pulse **Siguiente**, **Finalizar** y **Salir**.

6. Realice las mismas acciones en el siguiente NetScaler utilizando los valores para ese servidor.

7. En ambos servidores, vaya a **Gestión de tráfico > DNS > Registros > Registros A ** y examine la lista. Debería ver las entradas `root.servers.net` y su nombre de host con un tipo de Dominio de GSLB. 

8. Vaya a **Gestión de tráfico > DNS > Servidor de nombres** y pulse **Añadir**. Introduzca una dirección IP en el NetScaler (como por ejemplo la IP pública del dispositivo). Pulse **Local** y deje el protocolo como UDP. Pulse **Crear** y, a continuación, en **Cerrar**. Debería ver el estado efectivo como habilitado y activo.

9. Vaya a **Sistema > Red > IP** y abra las direcciones IP del GSLB. Asegúrese de que **Gestión** está seleccionado en ambas máquinas.

10. A continuación, en ambos servidores, vuelva a **Gestión de tráfico > GSLB** y siga el asistente de nuevo. Esta vez, pulse **Siguiente** y seleccione **Modificar la configuración de los dominios existentes**. Seleccione el nombre de host de la lista y, a continuación, pulse **Siguiente** dos veces. 

11. En el campo de dirección de sitio, introduzca la dirección IP del sitio del otro NetScaler, proporcione el nombre de sitio del otro NetScaler y pulse **Añadir**. El sitio se completará con una opción para pulsar de nuevo la '+' verde. Pulse el signo más del sitio remoto para añadir otro sitio. Introduzca la IP de servicio del servidor virtual (la de los servidores de equilibrio de carga, no la del sitio del GSLB) y el puerto, pulse **Crear** y **Cerrar**, **Siguiente**, **Finalizar** y **Salir**.

Si todo ha funcionado hasta aquí y ambos servidores están configurados, todo debería tener un estado verde en los servidores, servicios y sitios virtuales de GSLB. Observará que ahora hay dos entradas en los servicios de GSLB en ambas máquinas, si están debidamente sincronizadas. En este punto, los servidores están ahora comunicándose entre sí.

Ahora debe configurar los DNS.

En nuestro ejemplo, `gslb.tsstesting.com`, creará registros NS y de adherencia en la zona tsstesting.com:

    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; IP del servidor de nombres del primer NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; IP del servidor de nombres del segundo NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias para el objeto de GSLB en el dispositivo de NetScaler

Recuerde que solo puede utilizar CNAME con nombres de host y no la raíz del dominio.

Esta configuración establece los servidores de nombre para solicitudes de `gslb.tsstesting.com` a las IP de NetScaler para las que ha configurado el DNS. El registro CNAME convierte `tsstesting.com` en una solicitud de `gslb.tsstesting.com`. Por lo tanto, cualquier solicitud de `www.tsstesting.com` irá al NetScaler para resolverse y devolverá un registro basado en el método de equilibrio de carga que ha configurado.

Para obtener más información sobre el equilibrio de carga global de NetScaler, consulte:
* [Configuring the Netscaler for global load balancing ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://support.citrix.com/article/CTX110348){: new_window}
* [How DNS(Domain Name System) works with GSLB feature on NetScaler ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://support.citrix.com/article/CTX122619){: new_window}
* [Information on the MEP protocol and site monitoring ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://support.citrix.com/article/CTX111081){: new_window}

Hay otros productos que pueden ofrecer una funcionalidad similar para dispersar el tráfico en una base geográfica:

### CDN

Las redes de suministro de contenido (CDN) le permiten cargar o proporcionar un servidor de origen para servidores de memoria caché dispersos geográficamente, que proporcionan el contenido al cliente solicitante. Las CDN funcionan mejor con contenido extenso y estático como imágenes y vídeos que no cambian en el tiempo.

Para obtener información más detallada sobre las CDN, consulte la [documentación](https://console.bluemix.net/docs/infrastructure/CDN/getting-started.html#getting-started).

### Almacenamiento de objetos

El almacenamiento de objetos de {{site.data.keyword.BluSoftlayer_notm}} se puede configurar para utilizar varias ubicaciones geográficas en varios centros de datos para proporcionar contenido. Una aplicación que tiene en cuenta la ubicación puede realizar búsquedas de ubicación en la solicitud de cliente y devolver un URL al almacenamiento de objetos que está cerca del cliente. El almacenamiento de objetos también viene con un front-end de CDN, si es necesario, para proporcionar servicios de almacenamiento en memoria caché adicionales como se ha señalado anteriormente.

Para obtener más información y una introducción al almacenamiento de objetos, consulte la [documentación](https://console.bluemix.net/docs/services/cloud-object-storage/about-cos.html#about-ibm-cos). 
