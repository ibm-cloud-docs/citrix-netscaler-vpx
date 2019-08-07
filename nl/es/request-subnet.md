---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: subnet, private, request, vip

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

# Solicitar una subred privada
{: #request-a-private-subnet}

En la mayoría de los despliegues, el dispositivo {{site.data.keyword.vpx_full}} se despliega en una configuración de proxy inverso. Sin embargo, para configurar VPX con la configuración de proxy de reenvío, son necesarias IP virtuales (VIP), ya que la configuración existirá en una red privada en lugar de en una pública.

Debe crear una incidencia con el equipo de soporte de IBM© Cloud y solicitar que se añada a su cuenta una red privada del dispositivo de {{site.data.keyword.vpx_full}}. Tenga en cuenta que necesitará al menos dos direcciones privadas, por lo que debería solicitar como mínimo un tamaño de subred de /29.  
