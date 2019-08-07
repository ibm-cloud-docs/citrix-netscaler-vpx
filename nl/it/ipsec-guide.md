---

copyright:
  years: 2019
lastupdated: "2019-04-28"

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

# Configurazione della VPN site-to-site IPsec in {{site.data.keyword.vpx_full}} con IBM Virtual Router Appliance
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

Questa guida fornisce le istruzioni dettagliate per configurare una connessione site-to-site della VPN IPSec in Citrix VPX. Viene utilizzata una VRA (Virtual Router Appliance) di IBM come un peer VPN.

<img src="images/ipsec1.png" alt="immagine" style="width: 600px;"/>

## Informazioni sulla distribuzione
Questa distribuzione è stata creata e verificata con le seguenti specifiche del componente:

| Versione & Build NetScaler VPX	| Descrizione e versione VRA | 
| ------------- | ------------- | 
| NS12.1: Build 48.13.nc | AT&T vRouter 5600 1801q |

Hai bisogno di una licenza VPX Platinum per configurare la VPN IPSec.
{: note}

## Prima di cominciare

Questa guida presuppone che tu sia il proprietario di entrambi i dispositivi. Visita i seguenti link per le istruzioni sull'ordinazione.

-	[Introduzione all'applicazione software {{site.data.keyword.vpx_full}}](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[Introduzione a IBM Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## Quali operazioni eseguirai

In questa guida apprenderai come configurare una VPN IPSec nel dispositivo Citrix VPX.

Attività  | Descrizione
------------- | -------------
[Abilita le funzioni richieste in VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) | Per prima cosa, abilita le funzioni necessarie per creare la VPN IPSec.
[Crea un profilo IPSec](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile) | Il profilo IPSec include dei parametri di sicurezza per stabilire la connessione.
[Crea un tunnel IP](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) | In questa sezione creiamo un oggetto tunnel IP per specificare gli indirizzi IP locale e remoto, nonché i parametri del protocollo.
[Crea un PBR (Policy Based Routing)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing) | PBR viene utilizzato per definire i parametri del traffico univoci per le sottoreti locale e remota.
[Configura una VRA](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra) | Configura la VRA (Virtual Router Appliance), utilizzando la sintassi di configurazione VPN equivalente.
[Verifica lo stato della VPN](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection) | Verifica lo stato operativo della VPN ed effettua un semplice test di connettività.

## Risorse aggiuntive
Le risorse aggiuntive riportate di seguito possono aiutarti a ottenere maggiori informazioni su Citrix VPX e la VRA (Virtual Router Appliance).

* [CloudBridge Connector ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configuring a CloudBridge Connector tunnel between a Citrix ADC appliance and Cisco IOS device ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Documentazione di Citrix VPX/ADC 12.1 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [Documentazione VRA supplementare](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
