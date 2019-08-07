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

# Abilitazione delle funzioni richieste in {{site.data.keyword.vpx_full}}
{: #enable-required-features-in-vpx}

Puoi abilitare le funzioni richieste in VPX per creare la VPN IPSec:

1.	Accedi alla GUI (Graphical User Interface) VPX.
2.	Passa a **System > Settings > Configure Modes** e abilita **Layer 3 Mode (IP Forwarding)**.
3.	Vai a **System > Settings > Configure Advanced Features** e abilita **Cloud Bridge**.

Per abilitare queste funzioni nella CLI, immetti i seguenti comandi:

```
> enable ns feature CloudBridge
> enable ns mode L3

```

Per ulteriori istruzioni sulla connessione a NetScaler utilizzando la GUI o SSH, visita il [seguente articolo](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler)
