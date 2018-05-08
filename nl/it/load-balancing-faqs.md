---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

<a name="top"></a>
# Domande frequenti (FAQ)

Le seguenti sono le domande frequenti quando si usa Citrix NetScaler VPX.

## Cos'è Citrix NetScaler VPX?

Citrix NetScaler è un controller di distribuzione delle applicazioni che rende le applicazioni cinque volte migliori accelerando le prestazioni, garantendo la disponibilità e la protezione delle applicazioni e riducendo notevolmente i costi operativi. Scegli la migliore edizione di Citrix NetScaler che soddisfa i tuoi requisiti di applicazioni e distribuiscila sul sistema dedicato appropriato per le tue esigenze prestazionali. Per ulteriori informazioni su Citrix NetScaler, consulta la [pagina di NetScaler ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){: new_window}
sul sito web di Citrix.

## Perché è necessario il bilanciamento del carico?

Bilanciare il carico del traffico è diventato un aspetto chiave di molte implementazioni dei clienti poiché distribuisce le richieste e i carichi delle applicazioni su più server. Fornisce anche diversi vantaggi alla topologia nel suo complesso, tra cui:

* Sicurezza. L'isolamento logico dei server delle applicazioni viene creato o le richieste di traffico vengono negate in base ai protocolli IP e ai numeri porta.
* Alta disponibilità. Il contenuto viene replicato in un pool, o gruppo di server, garantendone la disponibilità per gli host.
* Scalabilità. È possibile aggiungere dei server aggiuntivi quando la domanda cresce, consentendo al programma di bilanciamento del carico di distribuire il carico di lavoro sui server aggiuntivi.
* Efficienza. I carichi di lavoro vengono distribuiti dinamicamente quando il bilanciamento del carico è configurato. Ad esempio, risorse come le CPU possono essere utilizzate in modi più efficienti.

## Quante opzioni di bilanciamento del carico sono disponibili in {{site.data.keyword.BluSoftlayer_notm}}?

Per un confronto dettagliato delle offerte di programmi di bilanciamento del carico di IBM, consulta [Explore Load Balancers](https://dev-console.bluemix.net/docs/infrastructure/loadbalancer-service/explore-load-balancers.html#explore-load-balancers).

## NetScaler supporta IPv6?

Sì. Sulla rete pubblica {{site.data.keyword.BluSoftlayer_notm}} sono supportai sia IPv6 che IPv4.

## NetScaler bilancerà il carico del traffico sulla rete privata?

Sì, NetScaler è il solo prodotto di bilanciamento del carico {{site.data.keyword.BluSoftlayer_notm}} che si estende alla rete privata.

## NetScaler può essere configurato per notificare l'indirizzo IP di origine del client invece dell'IP di origine dell'applicazione NetScaler?

Sì, il parametro **Use Source IP (USIP)** può essere impostato su **YES** nella NetScaler Advanced Management Interface per consentire la notifica dell'IP di origine del client invece di quello del NetScaler.

L'abilitazione della modalità di indirizzo USIP sull'applicazione aggiunge flessibilità all'applicazione stessa, consentendole di utilizzare l'indirizzo IP client, disponibile nell'intestazione IP, quando comunica con il server. Abilitando questa modalità, l'applicazione apre le connessioni server con l'indirizzo IP client e tiene inoltre conto dell'indirizzo IP client nel riutilizzo delle connessioni. Pertanto, questa modalità facilita un riutilizzo limitato per ogni singolo client basato sull'indirizzo IP client.

## Quali sono le diverse porte utilizzate per scambiare informazioni correlate all'alta disponibilità (HA, High Availability) tra i nodi in una configurazione HA?

La porta 3010, per la sincronizzazione e la propagazione dei comandi. La porta UDP 3003, per scambiare i pacchetti heartbeat.

## Quale versione di NetScaler VPX include GSLB (global server load balancing)?

Platinum.

## Posso avere NetScaler nella configurazione HA?

Sì, le applicazioni NetScaler VPX supportano le configurazioni di alta disponibilità (HA, High Availability).

I server NetScaler VPX non sono ridondanti, a meno che non siano configurati in modalità HA con un partner. Come parte della tua strategia di backup e ripristino, ti consigliamo vivamente di distribuire un ambiente HA, quando utilizzi NetScaler VPX.

È anche importante fornire la ridondanza per altri componenti hardware e software. Ad esempio, alimentatori e unità disco locali potrebbero non avere la ridondanza. Un malfunzionamento in tali componenti potrebbe tradursi in una perdita di dati.

## L'offerta {{site.data.keyword.BluSoftlayer_notm}} NetScaler include la funzionalità SSL VPN?

Sì, questa funzione è nota come NetScaler Gateway™ ed è inclusa in tutte le edizioni. Per ulteriori informazioni su questa funzione, visita il [sito web di Citrix ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.citrix.com/products/netscaler-adc/){: new_window}
