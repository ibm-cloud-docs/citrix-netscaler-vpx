---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurar Citrix Netscaler VPX como proxy de reenvío
{: #setting-up-citrix-netscaler-vpx-as-a-forwarding-proxy}

Un proxy de reenvío actúa como un único punto de control entre los clientes en una red interna e Internet. Un proxy permite al administrador de red o de seguridad la posibilidad de crear políticas que restringen el acceso a sitios de Internet.

Cuando un cliente en la red interna inicia una solicitud, la dirección IP del proxy se utilizará para iniciar la solicitud al servidor remoto en Internet. El servidor remoto responde al proxy, que devuelve la respuesta al cliente.

Normalmente, se combina un proxy con un cortafuegos para garantizar la seguridad de los clientes en una red interna.

## Paso 1: VIP de solicitud para utilizar en la red privada 

Cuando se pide un equilibrador de carga de Citrix NetScaler VPX desde el Portal de clientes de {{site.data.keyword.BluSoftlayer_notm}}, se presupone que se está solicitando un proxy inverso. Se le solicitará al solicitante el número de direcciones IP "públicas" a utilizar como IP virtual (VIP).

En el caso de un proxy de reenvío, las VIP deben configurarse en la red privada. Debe abrirse una incidencia de soporte para solicitar las VIP para la red privada. El número de VIP solicitado determinará el tamaño de la subred solicitada en la incidencia. La información de subred se devolverá en la incidencia.

En nuestro ejemplo hemos solicitado una subred `/29`, que ha dado lugar a lo siguiente:

* Subred creada `10.114.27.0/29` para utilizar como VIP privadas

* IP de subred (SNIP) `10.114.52.101` y subred direccionada `10.114.27.0/29`

* El equipo de soporte ha añadido las VIP `10.114.27.0-3` a Citrix NetScaler VPX

## Paso 2: Habilitar las características de equilibrio de carga y de redirección de memoria caché en Citrix NetScaler VPX

De forma predeterminada, las características de equilibrio de carga y redirección de la memoria caché en el equilibrador de carga de Citrix NetScaler VPX están inhabilitadas. El mandato `enable ns feature cr lb` las habilita.


## Paso 3: Crear el proxy de reenvío

Utilice la línea de mandatos para emitir los mandatos siguientes en el Citrix NetScaler VPX. En nuestro caso de ejemplo solo está habilitado uno de los dos servidores DNS de {{site.data.keyword.BluSoftlayer_notm}}.  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

La línea 1 crea la memoria caché de redirección. El protocolo es HTTP y `10.114.27.3` es una de las VIP solicitadas en la red privada. El puerto predeterminado es el 80 para HTTP, pero puesto que esta combinación de dirección y puerto va a utilizarse como sentencia proxy en el navegador, el puerto puede cambiarse según sea necesario.

La línea 2 añade una VIP de equilibrio de carga que representará el DNS "real".

La línea 3 añade la dirección IP del DNS "real" como servicio. Esta dirección puede ser el DNS del cliente o redireccionarse a los programas de resolución de DNS de {{site.data.keyword.BluSoftlayer_notm}}.

La línea 4 enlaza la VIP con el servidor "real". Todas las solicitudes de DNS a `10.114.27.4` se enviarán a `10.0.80.12`.

La línea 5 indica al servidor virtual de proxy de reenvío que utilice el DNS virtual para la resolución de nombres.

## Configuración del cliente

Antes de continuar personalizando el cliente para utilizar el proxy de reenvío, asegúrese de que no puede alcanzar un sitio público (por ejemplo, http://www.ibm.com) utilizando el navegador Firefox en el cliente. Dado que no habrá interfaz pública en el cliente, esta solicitud debe fallar. 

El ejemplo siguiente configura un cliente Linux.

Se deben realizar pocos cambios en el cliente. El primer cambio es apuntar al programa de resolución en el cliente al DNS virtual que puede hacerse de dos maneras.

Puede editar manualmente el archivo `/etc/resolv.conf` para que apunte a la dirección virtual del DNS. Tenga en cuenta que las herramientas de gestión del cliente pueden revertir estos cambios a los valores originales.  

O puede editar la interfaz `/etc/sysconfig/network-scripts/ifcfg-ethx` y añadir la sentencia `DNS1 =`. Una vez establecido, el mandato de reinicio de la red de servicio puede emitirse para recoger los cambios.

En cualquier caso, la dirección IP de DNS deberá configurarse como dirección DNS virtual y el navegador del cliente deberá configurarse para apuntar las solicitudes al proxy de reenvío de Citrix NetScaler VPX.

Utilice los siguientes pasos en Firefox para realizar los cambios necesarios:

1. Pulse **Preferencias > Avanzado > Red > Configuración de conexión**.

* Seleccione **Configuración de proxy manual** e introduzca lo siguiente:

  * **Dirección:** 10.114.27.3

  * **Puerto:** 80

  * Marque el recuadro de selección **Utilizar este servidor proxy para todos los protocolos**.

* Pulse **Guardar** y cierre la ventana del navegador.

La dirección IP `10.114.27.3` es la dirección IP de la memoria caché de reenvío creada en el paso 1.

En este punto, la configuración ha finalizado y puede acceder a Internet desde el recurso aislado en la red privada.

## Validación de la configuración

Ahora que el cliente está configurado para utilizar el proxy de reenvío, pruebe a acceder a un sitio público. La solicitud ahora debe ser satisfactoria.

Los siguientes mandatos de visualización pueden utilizarse para validar el estado del proxy de reenvío.

**show cr policy:** Muestra todas las políticas de redirección de memoria caché.

**show policy map:** Muestra las políticas de correlación configuradas y la información de política de correlación relacionada.

**show cr vserver:** Muestra un servidor virtual de redirección de memoria caché especificado o los muestra todos.

**stat cr vserver:** Muestra las estadísticas de servidor virtual de redirección de memoria caché.

La configuración de un proxy de reenvío básico en Citrix es bastante sencilla. Proporciona una forma de dar a los clientes una vía segura para recursos en Internet en una red interna. También permite al administrador de red mantener un nivel de control sobre la red.

Si se implementa en un sitio de cliente, es recomendable añadir un cortafuegos a la configuración para proteger mejor los recursos.
