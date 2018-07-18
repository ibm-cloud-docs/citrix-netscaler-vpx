---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Terminología

La plataforma Citrix NetScaler utiliza tanto terminología específica de producto como terminología y conceptos básicos del equilibrador de carga. 

### IP de NetScaler (NSIP)

La IP del equilibrador de carga designado para gestión.

### IP de subred (SNIP)

Una SNIP es la dirección IP de origen de un paquete utilizado por NetScaler cada vez que quiere comunicarse con un servidor (u objeto). Los servidores también utilizan la IP de subred para responder al NetScaler.

### IP virtual (VIP)

Una VIP es una dirección IP a la que un cliente envía solicitudes. NetScaler ha finalizado la conexión del cliente en la VIP y luego inicia una conexión con un servidor configurado en el servicio de equilibrio de carga.  Puede ser tanto una dirección IP pública para tráfico público (Internet) o una dirección IP privada para tráfico privado (intranet).

### Servidor virtual

Un servidor virtual, en términos de equilibrio de carga, hace referencia a la combinación de la dirección IP, el puerto y el protocolo al que un cliente IP se conecta y donde se envían las solicitudes de tráfico para una aplicación particular de la que NetScaler está equilibrando la carga.

### Servicio

La combinación de dirección IP, puerto y protocolo utilizada para direccionar las solicitudes a un servidor específico. Un servicio, una vez configurado, debe asociarse a un servidor virtual.

### Objeto de servidor

Una entidad virtual que le permite asignar un nombre significativo a un servidor físico, en lugar de utilizar su dirección IP normal.

### Supervisor

Un elemento que le permite realizar el seguimiento de un servicio, asegurando que funciona correctamente. El supervisor utiliza análisis y señales de latido para realizar un seguimiento del estado del servicio.
