---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, dns, security, check, configure

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Comprobar y configurar el registro DNS
{: #check-and-configure-the-dns-record}

En esta guía paso a paso de ejemplo, el servicio DNS de IBM© Cloud Internet Services se utiliza para gestionar la zona DNS y sus registros. En este caso, debe garantizar que se crea un registro del nombre de dominio completo que está en uso. El registro debe apuntar a la dirección pública que se debe configurar en el servidor virtual de Citrix Netscaler VPX.

<img src="images/12-add-record.png" alt="dibujo" style="width: 700px;"/>

La IP pública estática que se va a utilizar con Citrix VPX se puede recuperar en el portal de clientes en **Dispositivos > Lista de dispositivos** y seleccionando el nombre del Citrix Netscaler VPX.

<img src="images/13-check-ip.png" alt="dibujo" style="width: 300px;"/>
