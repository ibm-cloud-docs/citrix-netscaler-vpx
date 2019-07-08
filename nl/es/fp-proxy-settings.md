---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: proxy, update

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

# Actualizar los valores de proxy en el navegador de Internet de la máquina cliente (opcional)
{: #update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-}

Para actualizar los valores de proxy utilizando el navegador de Internet de la máquina cliente, realice los pasos siguientes:

1. Vaya a **Opciones de Internet** en los valores del navegador y configúrelas para que utilicen un servidor proxy en las solicitudes salientes.
2. Utilice la dirección IP del servidor virtual de redirección de memoria caché definida en los pasos anteriores como proxy.

Es posible que estos valores de proxy no sean necesarios si el dispositivo Citrix NetScaler VPX está en la vía de acceso directo de 3 capas entre máquinas cliente e Internet.
{: note}

<img src="images/fp17.png" alt="dibujo" style="width: 500px;"/>
