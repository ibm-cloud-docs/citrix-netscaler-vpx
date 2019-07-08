---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: terminology, nsip, snip, vip, service, object, monitor

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Terminología de Citrix NetScaler VPX
{: #citrix-netscaler-vpx-terminology}

La plataforma Citrix NetScaler utiliza tanto terminología específica de producto como terminología y conceptos básicos del equilibrador de carga.

### IP de NetScaler (NSIP)
{: #netscaler-ip-nsip-}

La IP del equilibrador de carga designado para gestión.

### IP de subred (SNIP)
{: #subnet-ip-snip-}

Una SNIP es la dirección IP de origen de un paquete utilizado por NetScaler cada vez que quiere comunicarse con un servidor (u objeto). Los servidores también utilizan la IP de subred para responder al NetScaler.

### IP virtual (VIP)
{: #virtual-ip-vip-}

Una VIP es una dirección IP a la que un cliente envía solicitudes. NetScaler ha finalizado la conexión del cliente en la VIP y luego inicia una conexión con un servidor configurado en el servicio de equilibrio de carga.  Puede ser tanto una dirección IP pública para tráfico público (Internet) o una dirección IP privada para tráfico privado (intranet).

### Servidor virtual
{: #virtual-server}

Un servidor virtual, en términos de equilibrio de carga, hace referencia a la combinación de la dirección IP, el puerto y el protocolo al que un cliente IP se conecta y donde se envían las solicitudes de tráfico para una aplicación particular de la que NetScaler está equilibrando la carga.

### Servicio
{: #service}

La combinación de dirección IP, puerto y protocolo utilizada para direccionar las solicitudes a un servidor específico. Un servicio, una vez configurado, debe asociarse a un servidor virtual.

### Objeto de servidor
{: #server-object}

Una entidad virtual que le permite asignar un nombre significativo a un servidor físico, en lugar de utilizar su dirección IP normal.

### Supervisor
{: #monitor}

Un elemento que le permite realizar el seguimiento de un servicio, asegurando que funciona correctamente. El supervisor utiliza análisis y señales de latido para realizar un seguimiento del estado del servicio.
