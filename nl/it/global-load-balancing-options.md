---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Bilanciamento del carico globale
{: #global-load-balancing}

Il bilanciamento del carico del server globale (GSLB, Global Server Load Balancing) è un metodo per suddividere il traffico su più server utilizzando DNS e le ubicazioni geografiche come strumenti per determinare dove deve essere inviato il traffico del server. In genere, un programma di bilanciamento del carico globale invia una richiesta client a un server che si trova più vicino al client, diminuendo la latenza e migliorando le prestazioni.

Potrebbe non servirti un'implementazione completa di una soluzione di bilanciamento del carico globale. GSLB richiede molteplici istanze di un dispositivo adatto in grado di eseguire questa funzione e, a seconda delle tue esigenze, potresti trovare più interessanti altre soluzioni. Se ti servono interi siti web e intere applicazioni, GSLB è una buona scelta. Se si servono solo parti del tuo contenuto, come ad esempio immagini, video o altri file di grandi dimensioni, una CDN ([Content Delivery Network](/docs/infrastructure/CDN?topic=CDN-about-content-delivery-networks-cdn-)) potrebbe essere più adatta (e più facile da distribuire).

## Citrix NetScaler VPX

Citrix NetScaler VPX è il solo dispositivo che può essere configurato dal cliente che esegue un reale bilanciamento del carico di lavoro globale. NetScaler è un'applicazione multifunzione che può eseguire ricerche di bilanciamento del carico di lavoro basate su DNS. Puoi puntare al NetScaler come un server DNS; il dispositivo controllerà i server di cui, secondo la sua configurazione, deve bilanciare il carico, eseguirà un calcolo delle distanze e restituirà un record con l'IP del server più vicino alla richiesta client.

Per il bilanciamento del carico globale, dovresti avere una configurazione dell'applicazione NetScaler in ogni data center. Ogni configurazione dell'applicazione NetScaler può essere un solo o una coppia di Netscaler in una coppia HA, a seconda dei tuoi requisiti, che fornisce dei servizi di bilanciamento del carico locali per i server dietro di loro. I dispositivi sono configurati per comunicare tra loro in modo da scambiare informazioni sullo stato su ciascun server assegnato alla rotazione del programma di bilanciamento del carico globale. Qualsiasi richiesta DNS che arriva su questi NetScaler configurati può restituire un corretto record per un server che è online e reattivo. Un server non reattivo viene rimosso dalla rotazione e ne viene selezionato una altro.

Devi già disporre del bilanciamento del carico configurato, anche se il bilanciamento riguarda solo un singolo server. Ti occorreranno degli ulteriori indirizzi IP per alcuni servizi, specificamente l'IP del sito GSLB. Questo IP viene utilizzato da NetScaler per comunicare con gli altri NetScaler nel protocollo di bilanciamento del carico globale. 

La seguente procedura di bilanciamento del carico utilizza:

### VPX1

`50.97.235.236` è denominato `VPX1Vserver` ed è il VIP di bilanciamento del carico locale per tale dispositivo. `50.23.66.52` sarà denominato `VPX1site` ed è l'IP locale per il GSLB di tale dispositivo.

### VPX2
`208.43.241.249` viene utilizzato per `VPX2Vserver` e l'IP GSLB è `208.43.224.4`, denominato `VPX2site`.

1. Vai a **Traffic Management > GSLB** e fai clic con il pulsante destro del mouse per abilitare la funzione. Seleziona quindi **Sites** e **Add**.

2. Sul primo dispositivo, immetti il nome (Name) come VPX1, il tipo (Type) come local (locale) e l'IP come `50.23.66.52` e seleziona quindi **Close**. 

	Dovresti vedere il sito elencato con uno stato verde. Non aggiungere ancora un sito remoto.

3. Vai a **Traffic Management > GSLB** e seleziona **GSLB Wizard**. Fai clic su **Next**. Immetti il nome host di cui bilancerai il carico (in questo esempio, `gslb.tsstesting.com`) Lascia il tipo di record (Record Type) come A e il tipo di servizio (Service Type) ANY. Il nome del server virtuale verrà compilato automaticamente. Fai clic su **Next**.

4. Scegli la tua forma di metodo di bilanciamento e persistenza proprio come faresti con il normale bilanciamento del carico. Fai clic su **Next**.

5. Il sito è già compilato, quindi non hai bisogno di aggiungere altro. Fai invece clic sul segno '+' verde accanto al nome del primo sito. Seleziona il server virtuale su tale dispositivo dall'elenco e fai clic su **Create**. Dovresti vedere che il sito è configurato con l'IP del sito e l'IP del server virtuale della tua configurazione con il carico bilanciato, e che è verde. Fai clic su **Next**, **Finish** e **Exit**.

6. Esegui le stesse azioni sul successivo NetScaler, utilizzando i valori per detto server.

7. Su entrambi i server, vai a **Traffic Management > DNS > Records > A records**, ed esamina l'elenco. Dovresti vedere delle voci `root.servers.net`, nonché il nome host, con un tipo di GSLB DOMAIN. 

8. Vai a **Traffic Management > DNS > Name Servers** e fai clic su **Add**. Immetti un indirizzo IP sul NetScaler (come ad esempio l'IP pubblico del dispositivo). Fai clic su **Local** e lascia il protocollo come UDP. Fai clic su **Create** e quindi su **Close**. Dovresti vedere lo stato effettivo come abilitato e attivo.

9. Vai a **System > Network > IPs** e apri l'indirizzo IP GSLB. Assicurati che **Management** sia selezionato per entrambe le macchine.

10. Quindi, su entrambi i server, torna a **Traffic Management > GSLB** e segui nuovamente la procedura guidata. Questa volta, fai clic su **Next** e seleziona **Modify Configuration for Existing Domains**. Seleziona il nome host dall'elenco e fai quindi clic su **Next** due volte. 

11. Nel campo dell'indirizzo del sito, inserisci l'indirizzo IP del sito dell'altro NetScaler, dagli il nome del sito dell'altro NetScaler e fai clic su **Add**. Il sito verrà compilato con un'opzione per fare clic nuovamente sul segno '+' verde. Fai clic sul segno più del sito remoto per aggiungere un altro sito. Immetti l'IP del servizio del server virtuale (quello per i server con il carico bilanciato, non l'IP del sito GSLB) e la porta, fai clic su **Create** e **Close**, **Next**, **Finish** e quindi su **Exit**.

Se tutto ha funzionato fino a questo punto, ed entrambi i server sono configurati, tutto dovrebbe avere uno stato verde nei siti, nei servizi e nei server virtuali GSLB. Noterai che ci sono ora due voci nei servizi GSLB su entrambe le macchine, se la loro sincronizzazione è corretta. A questo punto, i server stanno comunicando tra loro.

Ora devi configurare il DNS.

Nel nostro esempio, `gslb.tsstesting.com`, creerai NS e incollerai i record nella zona tsstesting.com:

    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; nameserver IP of first NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; nameserver IP of second NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias to the GSLB object on the NetScaler appliance

Ricordati che puoi utilizzare solo i CNAME con i nomi host, non la root del dominio.

Questa configurazione imposta i server dei nomi per le richieste per `gslb.tsstesting.com` agli IP NetScaler su cui hai configurato DNS. Il record CNAME converte `tsstesting.com` in una richiesta per `gslb.tsstesting.com`. Qualsiasi richiesta per `www.tsstesting.com` andrà quindi al NetScaler per essere risolta e restituirà quindi un record in base al metodo di bilanciamento del carico da te configurato.

Per ulteriori informazioni sul bilanciamento del carico globale NetScaler, fai riferimento a:
* [Configuring the Netscaler for global load balancing ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://support.citrix.com/article/CTX110348){: new_window}
* [How DNS(Domain Name System) works with GSLB feature on NetScaler ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://support.citrix.com/article/CTX122619){: new_window}
* [Information on the MEP protocol and site monitoring ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://support.citrix.com/article/CTX111081){: new_window}

Ci sono altri prodotti che possono offrire una funzionalità analoga per distribuire il traffico su una base geografica:

### CDN

Le CDN (Content Delivery Network) ti consentono di caricare o fornire un server di origine a server di cache distribuiti geograficamente che forniscono quindi il contenuto al client richiedente. Le CDN funzionano meglio con contenuti statici e in blocco, come ad esempio immagini e video che non cambiano nel corso del tempo.

Per ulteriori dettagli sulla CDN, consulta [questa documentazione](/docs/infrastructure/CDN?topic=CDN-getting-started).

### Object Storage

Object Storage di {{site.data.keyword.BluSoftlayer_notm}} può essere configurato per utilizzare più ubicazioni geografiche in diversi data center per fornire il contenuto. Un'applicazione in grado di riconoscere le aree geografiche può eseguire delle ricerche di ubicazioni sulla richiesta client e restituire un URL all'Object Storage vicino al client. Object Storage è fornito anche di un front-end CDN, se necessario, per fornire ulteriori servizi di memorizzazione in cache, come sopra indicato.

Per ulteriori informazioni e un'introduzione all'Object Storage, consulta [questa documentazione](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-about-ibm-cloud-object-storage). 
