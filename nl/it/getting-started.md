---
copyright:
  years: 1994, 2017
  
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione all'applicazione software Citrix NetScaler VPX
{: #getting-started-with-citrix-netscaler-vpx-software-appliance}

La distribuzione di un Citrix NetScaler VPX nella tua soluzione {{site.data.keyword.BluSoftlayer_notm}} accelera la distribuzione di applicazioni web, migliora le prestazioni e garantisce che le tue applicazioni e i tuoi servizi cloud rimangano ottimizzati, disponibili e protetti. Se hai dei carichi di lavoro impegnativi, come ad esempio giochi, big data e analisi, o dei cloud privati, Citrix NetScaler VPX può aiutarti a offrire la tua soluzione quando, dove e come serve di più ai tuoi utenti.

## Prima di cominciare
Per iniziare ad utilizzare Citrix NetScaler VPX, dovrai conoscere le seguenti informazioni:

* Le tue informazioni di accesso al Portale del cliente di IBM© Cloud
* L'ubicazione di distribuzione del tuo programma di bilanciamento del carico
* Quale tipo di Netscaler meglio soddisfa i tuoi bisogni (per ulteriori informazioni fai riferimento a [Esplora Load Balancers](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)
* Il numero di indirizzi IP pubblici necessari
* La VLAN dove vuoi assegnare il programma di bilanciamento del carico.

## Ordine di un Citrix NetScaler VPX

Per ordinare un'applicazione software Citrix NetScaler VPX, vai alla pagina degli ordini nel portale del cliente:

1. Dal tuo browser, apri il [Portale del cliente ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){: new_window} e accedi al tuo account.
2. Nella navigazione del portale del cliente, seleziona **Devices > Devices List** e fai clic sul link **Order Devices**. 
3. Nella pagina **Order SoftLayer Products and Services**, scorri verso il basso alla sezione Network e fai clic sul link **Order** in Citrix NetScaler VPX.
4. Dal menu a discesa, seleziona un'ubicazione (Location) dove desideri distribuire la tua applicazione software Citrix NetScaler VPX.  
5. Seleziona il miglior tipo NetScaler per la tua edizione e versione software e le tue esigenze di velocità effettiva. 
6. Seleziona il numero di indirizzi IP pubblici di cui hai bisogno.  
	Sono gli indirizzi IP pubblici statici, distribuiti come indirizzi VIP (Virtual IP) sul tuo NetScaler VPX.
7. Fai clic su **Continue**.
8. Immetti le informazioni richieste da ARIN (o dall'organizzazione equivalente nella tua regione di distribuzione) per gli indirizzi IP che hai richiesto.
9. Immetti le tue informazioni di contatto. 
10. Seleziona la tua VLAN. 
	Per ridurre al minimo la latenza e garantire un utilizzo ottimale delle tue risorse di rete, assegna Citrix NetScaler VPX alla stessa VLAN dei server dove verrà distribuito il traffico. 
11. Riesamina l'ordine, accetta i termini e fai clic su **Place Order**. L'applicazione software Citrix NetScaler VPX viene distribuita con le impostazioni da te selezionate. 

## Operazioni successive

Puoi scoprire di più sulle [funzioni](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-about-citrix-netscaler-vpx) di Citrix Netscaler VPX, rivedi la [terminologia](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-citrix-netscaler-vpx-terminology) di Netscaler specifica o inizia la [configurazione](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-basic-load-balancing-configuration) del tuo Netscaler.
