---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security

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

# Despliegue y configuración de IBM Hardware Security Module (HSM) con Citrix Netscaler VPX
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

Esta guía paso a paso le muestra la integración de HSM con Citrix Netscaler VPX. Después, los dos servicios podrán comunicar y generar el material criptográfico necesario para crear un certificado.

## Acerca del despliegue
{: #about-the-deployment}
El despliegue se ha creado y probado con las especificaciones de componente siguientes:

| Versión y compilación de NetScaler VPX	| Versión de software HSM | Versión de firmware de HSM | Versión de cliente HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: compilación 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

Si tiene una versión anterior de VPX o, si al solicitar el dispositivo a través de la plataforma IBM© Cloud, solo visualiza las versiones 11.1 y anteriores como opciones de selección, el dispositivo se podrá actualizar de modo que la configuración descrita en esta guía se pueda completar.
{: note}

## Topología lógica
{: #logical-topology}
En el diagrama siguiente se muestra el flujo de tráfico de red para el caso de uso de descarga SSL. Esto proporciona una perspectiva visual y lógica del enlace de confianza y de la configuración entre VPX y el dispositivo HSM.

<img src="images/network-flows-logical-topology.jpg" alt="dibujo" style="width: 700px;"/>

Si no está familiarizado con la descarga SSL, revise este [artículo de Citrix](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html).

## Qué conseguirá

{: #what-you-ll-accomplish}

En esta guía paso a paso aprenderá a desplegar y configurar un HSM con Citrix Netscaler VPX:

Tarea  | Descripción
------------- | -------------
[Solicitar un Módulo de seguridad de hardware (HSM)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) | En primer lugar, tendrá que solicitar un HSM.
[Solicitar Citrix Netscaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) | Si aún no lo ha hecho, deberá solicitar Citrix Netscaler VPX.
[Inicializar el HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) | La mayoría de las configuraciones requieren la inicialización del dispositivo HSM. Sin esto, solo se pueden ejecutar determinados mandatos `show`.
[Crear una partición](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition) | Una partición es un espacio lógico e independiente que está asociado o conectado al cliente que solicita o crea objetos criptográficos en el motor HSM.
[Instalar el software de cliente de HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software) | En esta subsección, el VPX se instalará con el software y los programas de utilidad necesarios para interactuar con el HSM. |
[Establecer el enlace de confianza de red (NTL)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) | Un enlace de confianza de red (NTL) es un canal seguro para que el gestor de servicios de hardware (HSM) y el cliente se comuniquen. |
[Crear claves y generar la solicitud de firma de certificado (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) | En esta subsección crearemos un par de claves que se utilizará para generar una Solicitud de firma de certificado (CSR) y para pedir/solicitar un certificado con la misma. |
[Solicitar el certificado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) | Solicitar un certificado SSL para Citrix Netscaler VPX.
[Recuperar y transferir el certificado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) | Recuperar el certificado SSL solicitado anteriormente y dejar todo listo para la instalación y configuración en la siguiente guía paso a paso.
