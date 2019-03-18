---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurazione del bilanciamento del carico di base
{: #basic-load-balancing-configuration}

Pensa a una società che ha un sito web di social community di base in cui gli utenti finali possono eseguire la registrazione per un account che non richiede informazioni sensibili e possono quindi accedere e pubblicare foto dei loro animali domestici. Ci sono tre server web/di applicazioni e un server di database che li supporta. Il dominio e il DNS sono ospitati con {{site.data.keyword.BluSoftlayer_notm}} e, poiché hanno un ambiente di piccole dimensioni, NetScaler e i server web/delle applicazioni si trovano tutti nella stessa VLAN. Questo semplifica le cose, poiché non è necessaria alcuna ulteriore configurazione perché NetScaler configuri una politica di bilanciamento del carico di base. La seguente procedura è una spiegazione semplificata al massimo del flusso di traffico in questa istanza:

1. Un utente immette l'URL nel suo browser.
2. Il record DNS dell'URL punta a uno dei VIP pubblici sul NetScaler.
3. Il NetScaler riceve il traffico su tale VIP e annota il protocollo del traffico utilizzato (traffico della porta HTTP 80).
4. Il NetScaler passa quindi il traffico a uno dei server nel pool di server, sulla base del metodo di bilanciamento del carico definito (round-robin, IP persistenza e così via).
5. Il server accetta quindi il traffico e l'utente si connette ed esegue l'accesso.

Per eseguire tale operazione, il NetScaler deve essere configurato per gestire questo traffico. Il fatto che il VIP, l'IP del server DNS e lo SNIP siano già configurati semplifica la configurazione. 

Nella GUI NetScaler, nella schermata Configuration, espandi **Traffic Management** sul lato sinistro. Espandi la sottosezione denominata **Load Balancing**. Indica quindi a NetScaler quali server di destinazione verranno inclusi nella politica di bilanciamento del carico attenendoti alla seguente procedura:

1. In Load Balancing, fai clic su **Servers**.
2. Fai clic su **Add**.
3. Immetti il nome del server (ad esempio, Web1).
4. Immetti l'indirizzo IP del server.
5. Lascia vuoto il campo **Traffic Domain** poiché a te interessa solo di utilizzare il dominio di traffico predefinito in questo scenario.
6. Immetti gli eventuali commenti che vuoi su questo server.
7. Fai clic su **Create**.

Ripeti questa procedura per tutti i server nel pool.  

**SUGGERIMENTO:** per fare in modo che i server rimangano facilmente identificabili, utilizza una convenzione di denominazione simile per i server nello stesso pool (ad esempio Web1, Web2, Web3 e così via).

Crea quindi i tuoi servizi. Creerai un servizio per ogni server da te appena immesso. Il servizio è quello che configura la connessione tra NetScaler e i server nel pool. Ogni servizio ha un nome e specifica un indirizzo IP, una porta e il tipo di dati fornito.

1. Fai clic su **Traffic Management > Load Balancing > Services**.
2. Fai clic su **Add**.
3. Crea un servizio per ciascun server da te creato in precedenza, utilizzando le stesse informazioni.

Crea quindi un Virtual Server. Il Virtual Server è una sorta di connessione virtuale tra il VIP utilizzato per i server con il carico bilanciato e i servizi da te creati in precedenza.

1. Fai clic su **Traffic Management > Load Balancing > Virtual Servers**.
2. Fai clic su **Add**.
3. Denomina il Virtual Server.
4. Indica il protocollo che bilancerai (HTTP).
5. Lascia il tipo di indirizzo IP (IP Address Type) sul valore predefinito (IP Address). Il campo dell'indirizzo IP è dove immetterai il VIP che utilizzerai come punto di ingresso per tutti i tuoi utenti.
6. Indica la porta. Il valore predefinito è la porta 80.
7. Fai clic su **OK**.

Associa quindi i servizi che hai creato al tuo Virtual Server.

1. Sulla schermata Virtual Servers, fai clic sul link **No Load Balancing Virtual Server Service Binding**.
2. Associa ciascuno dei servizi creati precedentemente al Virtual Server.
3. Fai clic su **Done**.
4. Fai clic sul pulsante **Refresh**. Lo stato (State) e lo stato effettivo (Effective State) verranno visualizzati come verdi.

Hai creato un pool di bilanciamento del carico e la politica per il tuo sito web.

**NOTA:** per ulteriori informazioni sulla configurazione del dispositivo Citrix NetScaler VPX, visita la [pagina di documentazione di Citrix![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/netscaler.html). Per ulteriore assistenza, contatta l'assistenza e il settore vendite di {{site.data.keyword.BluSoftlayer_notm}}.
