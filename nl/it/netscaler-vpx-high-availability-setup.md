---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: ha, high availability, setup, configure, configuration

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Configurazione di Citrix Netscaler VPX per l'alta disponibilità (HA, High Availability)
{: #setting-up-citrix-netscaler-vpx-for-high-availability-ha-}

I programmi di bilanciamento del carico vengono utilizzati per bilanciare il traffico su più server delle applicazioni per migliorare le prestazioni e la stabilità in un'applicazione scalabile. Eppure, un singolo programma di bilanciamento del carico è un singolo punto di malfunzionamento. Evitare tale condizione configurando una coppia Netscaler VPX ad alta disponibilità (HA, High Availability). La configurazione di una coppia HA richiede due server Netscaler VPX. Il server secondario subentra per continuare il bilanciamento del carico nel caso si verificasse un malfunzionamento di quello principale.

Lo SNIP (SubNet IP) è l'IP visto dai server con carico bilanciato come IP di origine delle richieste (connessioni) effettuate al VIP (Virtual IP) di NetScaler VPX. Di norma, in una configurazione di coppia HA, lo SNIP non subisce variazioni, ma è possibile che ciò si verifichi durante un evento di failover. Quando i due Netscaler sono nella stessa sottorete, è possibile che lo SNIP del NetScaler VPX secondario cambi nello SNIP originariamente utilizzato dal NetScaler VPX principale. Ciò non causerà alcuna confusione per i server che gestiscono la richiesta.

Per una configurazione HA, entrambi i NetScaler devono trovarsi nella stessa VLAN e sulla stessa sottorete.

Prima di iniziare la configurazione HA, assicurati di eseguire le seguenti azioni prerequisite:

1. Se la coppia sarà configurata attivo-attivo. qualsiasi sottorete VIP aggiunta alle istanze deve essere di tipo "Routed to VLAN" (Instradata a VLAN).
2. Se la coppia sarà configurata attivo-passivo, qualsiasi sottorete VIP aggiunge alle istanze deve essere "Routed to VLAN" (Instradata a VLAN) o "Secondary routed to IP" (Secondario instradato a IP) e instradata all'indirizzo IP pubblico del nodo principale.

Dopo aver ordinato i due server Netscaler VPX nella VLAN necessaria, e ordinato le sottoreti VIP e SNIP per soddisfare i prerequisiti per la tua configurazione di coppia HA, puoi procedere con le seguenti operazioni:

1. Apri due finestre del browser e accedi all'interfaccia avanzata su entrambi i NetScaler. Sul NetScaler secondario, vai a **System > User Administration > Users** e imposta la password root in modo che sia uguale a quella del NetScaler principale. Aggiorna quindi la password su file nel portale {{site.data.keyword.BluSoftlayer_notm}} nella pagina dei dettagli del dispositivo in modo che corrisponda alla password impostata per il secondario.

2. Sul VPX che vuoi che sia quello secondario, fai clic su **System > High Availability**, quindi fai clic con il pulsante destro del mouse sulla prima riga e fai clic su **Edit**. Seleziona **Stay Secondary** nella casella a discesa di configurazione dello stato di alta disponibilità e fai clic su **OK**.

3. Seleziona **Add**. Immetti l'indirizzo IP del sistema dell'altro VPX (si trova nella scheda High Availability sul principale) e immetti i dettagli di accesso root nella parte inferiore. Lascia la casella **Turn on INC** non selezionata. Fai clic su **OK**.

	Se ricevi un errore che indica che gli IP non sono nella stessa sottorete, è possibile che entrambi i server VPX non siano nella stessa VLAN. Altrimenti, dovresti ora essere in grado di aprire il server principale e selezionare il pulsante **Refresh** per vedere entrambi i server funzionanti ad alta disponibilità (HA, High Availability).

	Il nuovo IP di gestione NetScaler per il secondario sarà un singolo indirizzo IP più basso che in precedenza. Se non riesci a ottenere alcun accesso al VPX secondario, rimuovi l'alta disponibilità dalla riga di comando utilizzando:

	`sh ha node`

	Rimuovi quello che sarebbe il nodo ha:

	`rm ha node 1`

4. Sul VPX principale dovresti vedere che il VPX remoto sta ora eseguendo la sincronizzazione. Vai al server secondario e controlla la configurazione **Network > IPs**. Dovresti vedere il VIP del server principale e gli altri IP elencati come passivi.

6. Torna a **System > High Availability** sul server secondario e fai clic su **Edit**. Seleziona **ENABLED** nella casella a discesa e seleziona **OK**.

7. Forza un failover per eseguire un test. Aggiorna la schermata e osserva gli indirizzi IP diventare attivi sul secondario. Esegui nuovamente il failover e osservali diventare passivi. Esegui il ping degli IP per assicurarti che funzionino.

8. Il server principale dovrebbe ora essere etichettato come principale e quello secondario dovrebbe segnalare uno stato di sincronizzazione che indica una corretta esecuzione.
