---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Bilanciamento del carico globale con Citrix NetScaler VPX

Il bilanciamento del carico del server globale (GSLB, Global Server Load Balancing) è un meccanismo per distribuire il traffico su più server/istanze, che si trovano di norma in località geografiche differenti. L'idea è quella di avere un motore/server di bilanciamento globale che riceve le richieste di traffico dai client e li reindirizza a una specifica area geografica, che è determinata utilizzando i criteri/algoritmi selezionati e configurata dall'amministratore. Per ottenere questo risultato, all'interno della rete {{site.data.keyword.BluSoftlayer_notm}} possono essere utilizzati due metodi riconosciuti:

* La **CDN:** distribuisce contenuto e dati multimediali elaborati, quali immagini e video, e distribuisce geograficamente i contenuti su nodi dispersi mantenendo al tempo stesso la latenza minima e la velocità più elevata. Viene di norma implementata quando è necessario distribuire delle specifiche parti di contenuto, invece che interi siti web o intere applicazioni. {{site.data.keyword.BluSoftlayer_notm}} offre questo servizio; leggi ulteriori informazioni in merito [qui](https://console.bluemix.net/docs/infrastructure/CDN/getting-started.html#getting-started). 
* **NetScaler VPX:** come con un normale bilanciamento del carico locale, VPX utilizza una gerarchia degli oggetti simile per bilanciare il carico del traffico tra diverse aree geografiche. Utilizzando le ricerche locali basate su DNS, NetScaler sceglie il rispettivo record che corrisponde all'ubicazione/sito selezionati; la selezione è basata sui criteri preconfigurati dall'amministratore. Le sezioni successive descriveranno in modo più dettagliato questa opzione/offerta.

Nota che sono disponibili delle altre tecniche per la distribuzione di contenuto, come il reindirizzamento HTTP, che è anche possibile implementare con Citrix NetScaler VPX. 

## informazioni su GSLB su VPX

NetScaler VPX può essere abilitato con GSLB semplicemente attivando la sua funzione sulla CLI/GUI. 

GSLB utilizza componenti/oggetti molto simili a quelli utilizzati sulle distribuzioni di bilanciamento del carico locali, dove le entità sono definite utilizzando un modello gerarchico.

GSLB potrebbe essere implementato per diversi scopi. Alcuni potrebbero essere:

* **Condivisione/distribuzione del carico:** per distribuire le risorse in modo efficiente e intelligente tra più ubicazioni.
* **Ripristino di emergenza:** utilizzato quando l'ubicazione principale o primaria viene disattivata o non è in grado di offrire il servizio. In questo scenario, può subentrare un'ubicazione alternativa/di backup.
* **Modellamento delle prestazioni:** ciò ti consente di posizionare il contenuto più vicino ai sistemi finali o in un modo che migliora il servizio in questione.

I componenti o le entità principali nel processo o nella distribuzione GSLB sono:

* **Server virtuali:** un VIP è un indirizzo IP a cui i client inviano richieste; NetScaler termina la connessione client al VIP e avvia quindi una connessione a un server configurato nel servizio di bilanciamento del carico (locale). 
* **DNS (Domain Name System) e server di nomi:** la risoluzione dei nomi su GSLB funziona in modo molto simile a un normale DNS. La differenza è la logica/i criteri utilizzati per determinare l'indirizzo o gli indirizzi risolti; GSLB utilizza un metodo di bilanciamento del carico preconfigurato per gestire questa risoluzione. NetScaler può essere configurato per interagire con DNS in diversi modi:
	* ADNS (Authoritative DNS). I NetScaler che utilizzano la modalità ADNS sono autorevoli per uno specifico dominio e tutti i record su di esso.
	* Sottodelega DNS. Si verifica quando un server DNS (autorevole del dominio) delega la responsabilità di un dominio secondario a un sistema NetScaler.
	* Proxy DNS. Quando sono configurati in questa modalità, i NetScaler inoltrano le richieste DNS a un altro server (esterno) che gestisce la risoluzione dei nomi.
* **Metodo:** il metodo è un algoritmo che il server virtuale GSLB utilizza per selezionare il miglior servizio GSLB dalla topologia. L'algoritmo valuta gli aspetti relativi alle prestazioni che corrispondono agli effettivi criteri di selezione. Sono disponibili i seguenti metodi:
  * Round Robin: alterna le richieste in ingresso da gestire tra i siti/servizi GSLB, indipendentemente dal loro carico.
  * RTT (Round Trip Time): un lasso di tempo o un ritardo tra il server DNS locale del client e i siti (GSLB). NetScaler utilizza diversi meccanismi quali ICMP echo request/reply (PING), UDP e TCP per raccogliere le metriche RTT.
  * Static Proximity: utilizza un database di indirizzi IP per stabilire la prossimità tra il server DNS locale del client e i siti e lo utilizza quindi come criterio per operare una selezione.
  * Least Connections: misura il numero minimo di connessioni attive su ogni sito/servizio come criterio di selezione.
  * Least Response Time: seleziona il sito con il minor numero di connessioni attive e il tempo di risposta medio più basso.
  * Least Bandwidth: sceglie il sito che sta attualmente gestendo la quantità minore di traffico (Mbps).
  * Least Packets: seleziona il servizio che ha ricevuto il minor numero di pacchetti negli ultimi 14 secondi.
  * Source IP address Hash: opera una selezione del servizio in base al valore hash dell'indirizzo IPv4 o IPv6 client.
  * Custom Load: seleziona un servizio che non sta gestendo alcuna transazione attiva. Se tutti i servizi nella configurazione di bilanciamento del carico stanno gestendo delle transazioni attive, l'applicazione seleziona il servizio con il carico (utilizzo della CPU, memoria e tempo di risposta) minore.

* **MEP (Metric Exchange Protocol):** un protocollo proprietario utilizzato per scambiare metriche (carico e rete) e informazioni di persistenza tra i siti. MEP fornisce un controllo dell'integrità tra diversi siti/NetScaler nella rete mesh/topologia GSLB. Utilizzando i criteri impostati dall'amministratore, MEP fornisce ai siti un modo per comunicare e gestire il traffico in base ai parametri di selezione configurati precedentemente. MEP utilizza le porte TCP 3009 e 3011. Quando MEP è disabilitato, la selezione dei metodi è limitata alle opzioni elencate in precedenza e contrassegnate con un asterisco (*). Qualsiasi altro metodo scelto verrebbe reimpostato su Round Robin.
* **Monitoraggio:** il motore NetScaler valuta periodicamente lo stato dei servizi GSLB remoti utilizzando MEP oppure dei monitor espliciti associati ai servizi in questione. I monitor sono utilizzati proprio come su un servizio di bilanciamento del carico normale. Nel caso di GSLB, l'aggiunta di monitor ai servizi locali non è richiesta poiché tale controllo viene di norma eseguito da MEP. 
* **Persistenza:** una funzione facoltativa che stabilisce una preferenza di sito per uno specifico dominio. In questo particolare caso d'uso, il carico del traffico non viene bilanciato ma gestito dallo stesso data center. Ciò può essere utile in alcune applicazioni, come l'e-commerce, in cui i dati transazionali sono univoci per ciascun sito/server.
* **Sito GSLB:** i siti possono essere definiti come data center o ubicazioni in cui il sistema NetScaler è configurato/presente. Ogni sito GSLB è gestito da un sistema NetScaler che è considerato "locale" su tale sito, mentre tutti gli altri sistemi/siti remoti sono trattati come siti "remoti".
* **Servizio GSLB:** è un oggetto che rappresenta (ed è associato a) un VIP/server virtuale (normale). Può essere locale (stesso sito) o remoto.
* **Server virtuale GSLB:** un server virtuale GSLB viene assegnato a uno o più servizi GSLB che sarebbero di norma parte di siti (GSLB) differenti. Il carico del traffico ricevuto su di esso viene bilanciato tra i siti ad esso associati. La selezione del sito viene eseguita in base al metodo e al caso d'uso.
* **Dominio GSLB:** rappresenta il dominio o la zona di cui è responsabile il server virtuale GSLB. 
* **Servizio ADNS:** un servizio rappresentato da una combinazione di indirizzo IP e porta; è dove vengono inviate le richieste DNS a un dominio per cui NetScaler ha un ruolo autorevole. NetScaler le porta al server virtuale GSLB associato a tale dominio per ottenere una risposta.
