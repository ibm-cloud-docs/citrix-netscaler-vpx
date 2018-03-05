---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Acceso y gestión de Citrix NetScaler VPX

Los dispositivos Citrix NetScaler son herramientas potentes con una matriz de características que ayudan a mejorar y refinar la solución de {{site.data.keyword.BluSoftlayer_notm}} de muchas maneras. Puede encontrar la información del dispositivo en el portal del cliente y conectarse al dispositivo y configurar sus características.  

## Encontrar los detalles de NetScaler en el portal de cliente

Los dispositivos de Citrix NetScaler están listados en la lista de dispositivos, como cualquier otro servidor que tenga en la plataforma de {{site.data.keyword.BluSoftlayer_notm}}.

Para encontrar la lista de dispositivos:

1. En el navegador, abra el [Portal del cliente ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window} e inicie sesión en su cuenta. 
2. En la navegación del portal del cliente, seleccione **Dispositivos > Lista de dispositivos**.

Verá los dispositivos, ordenados por nombre de dispositivo. Los dispositivos de Citrix NetScaler VPX tienen el tipo de dispositivo "NetScaler". 

En el lado izquierdo de la fila de NetScaler, pulse la flecha para ampliar la línea y mostrar el nombre de usuario y una contraseña enmascarados para acceder a la gestión de NetScaler. 

Otros detalles en la Lista de dispositivos incluyen: 

* Ubicación (centro de datos en el que reside NetScaler)
* Dirección IP privada (utilizada para conectarse con NetScaler para funciones de gestión)
* Fecha de inicio (cuándo se ha pedido la máquina y suministrado)

**NOTA:** Aunque la dirección IP privada de NetScaler aparece en el portal, la pública no. Esto se debe a que la gestión de NetScaler se realiza utilizando la dirección IP privada y las direcciones IP públicas para dispositivos NetScaler se utilizan como VIP del dispositivo o IP virtuales, utilizadas para los servicios de equilibrio de carga.

## Pantalla Detalles del dispositivo 

Al pulsar el nombre de NetScaler, le lleva a la página **Detalles del dispositivo** de NetScaler, que muestra la VLAN en la que se despliega el NetScaler, así como sus direcciones IP públicas. Estas direcciones IP no pueden utilizarse para la gestión, porque son las direcciones VIP públicas predeterminadas de NetScaler. Las utilizará más tarde para asociar a un servicio para fines de equilibrio de carga.

## Gestión del NetScaler

{{site.data.keyword.BluSoftlayer_notm}} concede acceso raíz completo a su dispositivo NetScaler. Para iniciar sesión en la IU de gestión de NetScaler, debe estar conectado a la red privada de {{site.data.keyword.BluSoftlayer_notm}} (VPN de gestión de {{site.data.keyword.BluSoftlayer_notm}} o realizar funciones de gestión desde una sesión remota en un servidor dentro del entorno de {{site.data.keyword.BluSoftlayer_notm}}). 

Para conectarse desde el portal de cliente a la IU de gestión de NetScaler, pulse la lista desplegable de **Acciones** en la esquina superior derecha de la pantalla de **Detalles del dispositivo** y elija **Gestionar dispositivo** para iniciar un nuevo separador o una ventana emergente en el navegador. Esto le direcciona a la NSIP de NetScaler (la dirección IP privada que vio anteriormente). La página que se muestra le solicita el nombre de usuario root y la contraseña para el dispositivo. Una vez que especifique la información, le llevará a la GUI de gestión de NetScaler. 

Como alternativa, puede copiar y pegar la dirección IP privada del dispositivo NetScaler en un navegador web.

### Acceso SSH a NetScaler

También puede conectarse con el dispositivo NetScaler directamente utilizando su cliente SSH favorito. Utilice la dirección IP privada y la información de inicio de sesión del dispositivo NetScaler de la página Lista de dispositivos y asegúrese de que está conectado a la VPN de {{site.data.keyword.BluSoftlayer_notm}}. 
