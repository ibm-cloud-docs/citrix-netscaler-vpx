---
copyright:
  years: 1994, 2019

lastupdated: "2019-06-11"

keywords: manage, managing, locating, details, portal, device, list

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Gestionar {{site.data.keyword.vpx_full}}
{: #managing-your-citrix-netscaler-vpx}

Los dispositivos Citrix NetScaler son herramientas potentes con una matriz de características que ayudan a mejorar y refinar la solución de {{site.data.keyword.cloud}} de muchas maneras. Puede encontrar la información del dispositivo en el portal de clientes de la infraestructura de {{site.data.keyword.cloud_notm}} y conectarse al dispositivo y configurar sus características.  

## Encontrar los detalles de NetScaler en el portal de clientes
{: #locating-netscaler-details-in-the-customer-portal}

Los dispositivos de Citrix NetScaler están listados en la lista de dispositivos, como cualquier otro servidor que tenga en la plataforma de {{site.data.keyword.cloud_notm}}.

Para encontrar la lista de dispositivos:

1. En el navegador, abra el [portal de clientes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window} e inicie sesión en su cuenta.
2. En la navegación del portal de clientes, seleccione **Dispositivos > Lista de dispositivos**.

Verá los dispositivos, ordenados por nombre de dispositivo. Los dispositivos de {{site.data.keyword.vpx_full}} tienen el tipo de dispositivo "NetScaler".

En el lado izquierdo de la fila de NetScaler, pulse la flecha para ampliar la línea y mostrar el nombre de usuario y una contraseña enmascarados para acceder a la gestión de NetScaler.

Otros detalles en la Lista de dispositivos incluyen:

* Ubicación (centro de datos en el que reside NetScaler)
* Dirección IP privada (utilizada para conectarse con NetScaler para funciones de gestión)
* Fecha de inicio (cuándo se ha pedido la máquina y suministrado)

Aunque la dirección IP privada de NetScaler aparece en el portal, la pública no. Esto se debe a que la gestión de NetScaler se realiza utilizando la dirección IP privada y las direcciones IP públicas para dispositivos NetScaler se utilizan como VIP del dispositivo o IP virtuales, utilizadas para los servicios de equilibrio de carga.
{: note}

## Pantalla Detalles del dispositivo
{: #the-device-details-screen}

Al pulsar el nombre de NetScaler, le lleva a la página **Detalles del dispositivo** de NetScaler, que muestra la VLAN en la que se despliega el NetScaler, así como sus direcciones IP públicas. Estas direcciones IP no pueden utilizarse para la gestión, porque son las direcciones VIP públicas predeterminadas de NetScaler. Las utilizará más adelante para asociarse a un servicio de equilibrio de carga.

## Conexión a NetScaler
{: #connecting-to-the-netscaler}

{{site.data.keyword.cloud_notm}} concede acceso raíz completo a su dispositivo NetScaler. Para iniciar sesión en la IU de gestión de NetScaler, debe estar conectado a la red privada de {{site.data.keyword.cloud_notm}} (VPN de gestión de {{site.data.keyword.BluSoftlayer_notm}} o realizar funciones de gestión desde una sesión remota en un servidor dentro del entorno de {{site.data.keyword.cloud_notm}}).

Para conectarse desde el portal de clientes a la IU de gestión de NetScaler, pulse la lista desplegable de **Acciones** en la esquina superior derecha de la pantalla de **Detalles del dispositivo** y elija **Gestionar dispositivo** para iniciar un nuevo separador o una ventana emergente en el navegador. Esto le direcciona a la NSIP de NetScaler (la dirección IP privada que vio anteriormente). La página que se muestra le solicita el nombre de usuario root y la contraseña para el dispositivo. Una vez que especifique la información, le llevará a la GUI de gestión de NetScaler.

Como alternativa, puede copiar y pegar la dirección IP privada del dispositivo NetScaler en un navegador web.

### Acceso SSH a NetScaler
{: #netscaler-ssh-access}

También puede conectarse con el dispositivo NetScaler directamente utilizando su cliente SSH favorito. Utilice la dirección IP privada y la información de inicio de sesión del dispositivo NetScaler de la página Lista de dispositivos y asegúrese de que está conectado a la VPN de {{site.data.keyword.cloud_notm}}.
