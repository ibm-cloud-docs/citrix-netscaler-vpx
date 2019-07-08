---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: terminology, nsip, snip, vip, service, object, monitor

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Terminologia di Citrix NetScaler VPX
{: #citrix-netscaler-vpx-terminology}

La piattaforma Citrix NetScaler utilizza sia una terminologia specifica per il prodotto sia una terminologia e concetti del programma di bilanciamento del carico di base.

### NSIP (NetScaler IP)
{: #netscaler-ip-nsip-}

L'IP del programma di bilanciamento del carico indicato per fini gestionali.

### SNIP (SubNet IP)
{: #subnet-ip-snip-}

Uno SNIP è l'indirizzo IP di origine di un pacchetto utilizzato da NetScaler ogni volta che vuole comunicare con un server (o un oggetto). I server utilizzano lo SNIP (SubNet IP) anche per rispondere a NetScaler.

### VIP (Virtual IP)
{: #virtual-ip-vip-}

Un VIP è un indirizzo IP a cui un client invia le richieste. NetScaler ha terminato la connessione client al VIP e avvia quindi una connessione a un server configurato nel servizio di bilanciamento del carico.  Può essere un indirizzo IP pubblico per il traffico pubblico (internet) oppure un indirizzo IP privato per il traffico privato (intranet).

### Virtual Server
{: #virtual-server}

Un Virtual Server, in termini di bilanciamento del carico, fa riferimento alla combinazione di indirizzo IP, porta e protocollo a cui un client IP si connette e dove vengono inviate le richieste di traffico per una specifica applicazione di cui NetScaler sta bilanciando il carico.

### Servizio
{: #service}

La combinazione di indirizzo IP, porta e protocollo utilizzata per instradare le richieste a uno specifico server. Un servizio, una volta configurato, deve essere poi associato a un Virtual Server.

### Oggetto server
{: #server-object}

Un'entità virtuale che ti consente di assegnare un nome descrittivo a un server fisico invece di utilizzarne il normale indirizzo IP.

### Monitor
{: #monitor}

Un elemento che ti consente di tenere traccia di un servizio, garantendo che stia funzionando correttamente. Il monitor utilizza probe e segnali di heartbeat per tenere traccia dello stato del servizio.
