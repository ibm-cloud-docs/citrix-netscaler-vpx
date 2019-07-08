---

copyright:
  years: 2019
lastupdated: "2019-04-08"

keywords: ipsec, vpn, vpx, tunnel

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

# Habilitar las características obligatorias en Citrix Netscaler VPX
{: #enable-required-features-in-vpx}

Puede habilitar las características necesarias en VPX para crear la VPN de IPSec:

1.	Acceda a la GUI (interfaz gráfica de usuario) de VPX.
2.	Vaya a **Sistema > Valores > Configurar Modalidades** y habilite **Modalidad de Capa 3(Reenvío de IP)**.
3.	Vaya a **Sistema > Valores > Configurar características avanzadas** y habilite **Cloud Bridge**.

Para habilitar estas características en la CLI, ejecute los mandatos siguientes:

```
> enable ns feature CloudBridge
> enable ns mode L3

```

Para obtener instrucciones adicionales sobre cómo conectarse a NetScaler utilizando la GUI o SSH, visite [este artículo](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler)
