---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: proxy, traffic, appliance

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

# Configurazione del reindirizzamento del traffico del proxy di inoltro utilizzando l'applicazione Citrix NetScaler VPX
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

Questa guida ti fornisce una configurazione passo dopo passo per l'impostazione di un proxy di inoltro utilizzando l'applicazione Citrix NetScaler VPX. Questa configurazione è stata verificata su un'applicazione Citrix NetScaler VPX su cui è in esecuzione una versione software 11.1 (Platinum Edition) e prestazioni 10Mbps.

<img src="images/fp1.png" alt="immagine" style="width: 600px;"/>

## Quali operazioni eseguirai
{: #what-you-ll-accomplish}

In questa guida passo dopo passo, apprenderai come configurare il servizio:

Attività  | Descrizione
------------- | -------------
[Ordinazione di Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) | Inizia ordinando un'applicazione Citrix NetScaler VPX.
[Richiesta di una sottorete privata](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) | Richiedi una sottorete privata dal supporto IBM© per il tuo account.
[Abilitazione delle funzioni di reindirizzamento della cache e di bilanciamento del carico](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) | Identifica le risorse della tua applicazione, ad esempio i pool di origine e i meccanismi del controllo di integrità.
[Configurazione del server virtuale DNS](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) | Aggiungi i tuoi resolver DNS, definisci il tuo gruppo di servizi DNS, quindi definisci il tuo server virtuale DNS.
[Configurazione del reindirizzamento della cache per il traffico HTTP(S)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic) | Configura il reindirizzamento della cache per il tuo server virtuale del proxy di inoltro con il traffico HTTP o HTTPS.
[Configurazione del reindirizzamento della cache per il traffico SSL (Facoltativo)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) | Configura il reindirizzamento della cache per il tuo server virtuale del proxy di inoltro con il traffico SSL invece di HTTP o HTTPS.
[Configurazione del NAT di origine per il traffico in uscita](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) | Utilizza la tua applicazione Citrix NetScaler VPX per eseguire NAT sul traffico in uscita dalle tue macchine client.
[Aggiornamento delle impostazioni proxy sul browser Internet della macchina client (Facoltativo)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) | Aggiorna le tue impostazioni proxy utilizzando il browser internet della tua macchina client, se lo desideri.
