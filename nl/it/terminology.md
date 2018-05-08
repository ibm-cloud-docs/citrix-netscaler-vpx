---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Terminologia

La piattaforma Citrix NetScaler utilizza sia una terminologia specifica per il prodotto sia una terminologia e concetti del programma di bilanciamento del carico di base. 

### NSIP (NetScaler IP)

L'IP del programma di bilanciamento del carico indicato per fini gestionali.

### SNIP (SubNet IP)

Uno SNIP è l'indirizzo IP di origine di un pacchetto utilizzato da NetScaler ogni volta che vuole comunicare con un server (o un oggetto). I server utilizzano lo SNIP (SubNet IP) anche per rispondere a NetScaler.

### VIP (Virtual IP)

Un VIP è un indirizzo IP a cui un client invia le richieste. NetScaler ha terminato la connessione client al VIP e avvia quindi una connessione a un server configurato nel servizio di bilanciamento del carico. Può essere un indirizzo IP pubblico per il traffico pubblico (internet) oppure un indirizzo IP privato per il traffico privato (intranet).

### Server virtuale

Un server virtuale, in termini di bilanciamento del carico, fa riferimento alla combinazione di indirizzo IP, porta e protocollo a cui un client IP si connette e dove vengono inviate le richieste di traffico per una specifica applicazione di cui NetScaler sta bilanciando il carico.

### Servizio

La combinazione di indirizzo IP, porta e protocollo utilizzata per instradare le richieste a uno specifico server. Un servizio, una volta configurato, deve essere poi associato a un server virtuale.

### Oggetto server

Un'entità virtuale che ti consente di assegnare un nome descrittivo a un server fisico invece di utilizzarne il normale indirizzo IP.

### Monitor

Un elemento che ti consente di tenere traccia di un servizio, garantendo che stia funzionando correttamente. Il monitor utilizza probe e segnali di heartbeat per tenere traccia dello stato del servizio.
