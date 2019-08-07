---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, retrieve, transfer, certificate

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

# Recuperar y transferir el certificado
{: #retrieve-and-transfer-the-certificate}

Recupere el certificado SSL que ha solicitado anteriormente para estar preparado para la instalación y configuración en la siguiente guía paso a paso [Configuración y ajuste de la descarga SSL con {{site.data.keyword.vpx_full}}](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx).

1. Poco después de validar la propiedad del dominio, debería recibir un correo electrónico confirmando la finalización del cumplimiento del certificado y del propio certificado.

	Copie el texto de `---BEGIN CERTIFICATE---` hasta `---END CERTIFICATE---` y guarde el contenido como un nuevo archivo de certificado con la extensión `.cer`.

2. Copie el archivo de certificado en el directorio `/nsconfig/ssl` en {{site.data.keyword.vpx_full}}.

  <img src="images/11-transfer-certificate.png" alt="dibujo" style="width: 600px;"/>

{{site.data.keyword.vpx_full}} ahora está preparado para incorporar el certificado en un despliegue de equilibrio de carga utilizando SSL.
