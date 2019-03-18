---

copyright:
  years: 2018
lastupdated: "2018-11-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configuración y ajuste de la descarga SSL con Citrix Netscaler VPX
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

Esta guía paso a paso le dirige a través de la configuración y ajuste de la descarga SSL en Citrix Netscaler VPX; esto se lleva a cabo utilizando el certificado y el material criptográfico generado a través del enlace de HSM.

**NOTA:** Esta guía paso a paso presupone que ha completado los pasos de [Despliegue y configuración de IBM© Hardware Security Module (HSM) con Citrix Netscaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) para pedir y crear el emparejamiento VPX/HSM.

## Acerca del despliegue
El despliegue se ha creado y probado con las especificaciones de componente siguientes:

| Versión y compilación de NetScaler VPX	| Versión de software HSM | Versión de firmware de HSM | Versión de cliente HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: compilación 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## Topología lógica
En el diagrama siguiente se muestra el flujo de tráfico de red para el caso de uso de descarga SSL. Esto proporciona una perspectiva visual y lógica del enlace de confianza y de la configuración entre Citrix VPX y el dispositivo HSM.

<img src="images/network-flows-logical-topology.jpg" alt="dibujo" style="width: 700px;"/>

Si no está familiarizado con la descarga SSL, revise este artículo de [Citrix ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}.

## Qué conseguirá

En esta guía paso a paso aprenderá a configurar el SSL para Citrix Netscaler VPX:

Tarea  | Descripción
------------- | -------------
[Instalar el certificado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) | Instale el certificado SSL que ha creado en la [guía paso a paso](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) anterior.
[Comprobar y configurar el registro DNS](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | Asegúrese de que existe un registro DNS para el FQDN que apunta a la dirección pública que se debe configurar en Citrix Netscaler VPX como servidor virtual.
[Añadir y configurar el servidor virtual SSL](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | Añadir y configurar un servidor virtual SSL.
[Crear y aplicar una nueva suite de cifrado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | Cree una suite de cifrado que dé prioridad y preferencia a AEAD, ECDHE y ECDSA.

## Recursos adicionales
Los siguientes recursos adicionales puede ayudarle a sacar el máximo rendimiento de Citrix Netscaler VPX al utilizar IBM Hardware Security Module.

* [NetScaler 12.1 Documentación del producto ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Portal de soporte de Gemalto ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [Soporte de IBM Cloud](https://{DomainName}/docs/get-support?topic=get-support-using-avatar){:new_window}
