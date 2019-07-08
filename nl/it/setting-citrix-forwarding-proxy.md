---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"

keywords: setup, proxy, forward, vip, subnet

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Configurazione di Citrix Netscaler VPX come un proxy di inoltro
{: #setting-up-citrix-netscaler-vpx-as-a-forwarding-proxy}

Un proxy di inoltro funge da singolo punto di controllo tra i client su una rete interna e internet. Un proxy consente all'amministratore di rete o a quello della sicurezza di creare delle politiche che limitano l'accesso ai siti internet.

Quando un client nella rete interna avvia una richiesta, l'indirizzo IP del proxy verrà utilizzato per avviare la richiesta al server remoto su internet. Il server remoto a sua volta risponde al proxy, che restituisce la risposta al client.

Di norma, un proxy è combinato con un firewall per garantire la sicurezza dei client in una rete interna.

## Passo 1: Richiedere i VIP da utilizzare nella rete privata
{: #step-1-request-vips-to-use-in-the-private-network}

Quando un programma di bilanciamento del carico Citrix NetScaler VPX viene ordinato dal portale del cliente {{site.data.keyword.BluSoftlayer_notm}}, si presume che si stia richiedendo un proxy inverso. Al richiedente verrà chiesto il numero di IP "pubblici" da utilizzare come VIP (Virtual IP).

Nel caso di un proxy di inoltro, i VIP devono essere configurati sulla rete privata. È necessario aprire un ticket di supporto per richiedere i VIP per la rete privata. Il numero di VIP necessario determinerà la dimensione della sottorete richiesta nel ticket. Le informazioni sulla sottorete verranno restituite nel ticket.

Nel nostro esempio, abbiamo richiesto una sottorete `/29` e il risultato è stato il seguente:

* È stata creata la sottorete `10.114.27.0/29` per l'utilizzo come VIP privati

* SNIP (Subnet IP) `10.114.52.101` e sottorete instradata `10.114.27.0/29`

* I VIP `10.114.27.0-3` sono stati aggiunti a Citrix NetScaler VPX dal team di supporto

## Passo 2: Abilitare le funzioni di bilanciamento del carico e di reindirizzamento della cache su Citrix NetScaler VPX
{: #step-2-enable-load-balancing-and-cache-redirect-features-on-the-citrix-netscaler-vpx}

Per impostazione predefinita, le funzioni di bilanciamento del carico e di reindirizzamento della cache sul programma di bilanciamento del carico Citrix NetScaler VPX sono disabilitate; il comando `enable ns feature cr lb` le abilita.


## Passo 3: Creare il proxy di inoltro
{: #step-3-create-the-forward-proxy}

Utilizzare la riga di comando per immettere i seguenti comandi su Citrix NetScaler VPX. Nel nostro scenario, viene aggiunto solo uno dei due server DNS {{site.data.keyword.BluSoftlayer_notm}}.  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

La riga 1 crea la cache di reindirizzamento. Il protocollo è HTTP e `10.114.27.3` è uno dei VIP richiesti sulla rete privata. La porta è quella predefinita 80 per HTTP ma, poiché questa combinazione di indirizzo e porta verrà utilizzata come istruzione proxy nel browser, è possibile modificare la porta come necessario.

La riga 2 aggiunge un VIP di bilanciamento del carico che rappresenterà il DNS "reale".

La riga 3 aggiunge l'indirizzo IP del DNS "reale" come un servizio. Questo indirizzo può essere il DNS del cliente oppure instradato nuovamente ai resolver DNS forniti da {{site.data.keyword.BluSoftlayer_notm}}.

La riga 4 associa il VIP al server "reale". Tutte le richieste DNS a `10.114.27.4` verranno inviate a `10.0.80.12`.

La riga 5 indica al server virtuale proxy di inoltro di utilizzare il DNS virtuale per la risoluzione dei nomi.

## Configurazione del client
{: #configuring-the-client}

Prima di continuare la personalizzazione del client per l'uso del proxy di inoltro, assicurati di non poter raggiungere un sito pubblico (ad esempio, http://www.ibm.com) utilizzando il browser Firefox sul client. Poiché non ci deve essere alcuna interfaccia pubblica sul client, questa richiesta non riuscirà.

Il seguente esempio configura un client Linux.

È necessario apportare alcune modifiche al client. la prima modifica consiste nel puntare il resolver sul client al DNS virtuale; puoi eseguire tale operazione in due modi.

Puoi modificare manualmente `/etc/resolv.conf` per puntare all'indirizzo virtuale del DNS. Tieni presente che gli strumenti di gestione del client potrebbero annullare tali modifiche ripristinando le impostazioni originali.  

In alternativa, puoi modificare l'interfaccia `/etc/sysconfig/network-scripts/ifcfg-ethx` e aggiungere l'istruzione `DNS1=`. Una volta eseguita l'impostazione, è possibile immettere il comando service network restart per rilevare le modifiche.

In entrambi i casi, l'indirizzo IP del DNS dovrà essere configurato come indirizzo DNS virtuale e il browser del client dovrà essere configurato per puntare le richieste al proxy di inoltro di Citrix NetScaler VPX.

Per apportare le modifiche necessarie, esegui le seguenti operazioni in Firefox:

1. Fai clic su **Preferenze > Avanzate > Rete > Impostazioni connessione**.

* Seleziona **Configurazione proxy manuale** e immetti quanto segue:

  * **Indirizzo:** 10.114.27.3

  * **Porta:** 80

  * Seleziona la casella di spunta **Utilizza questo server proxy per tutti i protocolli**.

* Fai clic su **Salva** e chiudi la finestra del browser.

L'indirizzo IP `10.114.27.3` è quello della cache di inoltro creata al Passo 1.

A questo punto, la configurazione è completa e puoi accedere a internet dalla risorsa isolata sulla rete privata.

## Convalida della configurazione
{: #validating-the-setup}

Ora che il client è configurato per utilizzare il proxy di inoltro, prova nuovamente ad accedere a un sito pubblico. la richiesta ora dovrebbe riuscire.

Puoi usare i seguenti comandi di visualizzazione per convalidare lo stato del proxy di inoltro.

**show cr policy:** Visualizza tutte le politiche di reindirizzamento della cache esistenti.

**show policy map:** Visualizza le politiche di associazione che sono state configurate e le informazioni sulle politiche di associazione correlate.

**show cr vserver:** Visualizza uno specifico server virtuale di reindirizzamento della cache oppure tutti i server virtuali di reindirizzamento della cache configurati.

**stat cr vserver:** Visualizza le statistiche del server virtuale di reindirizzamento della cache.

La configurazione di un proxy di inoltro di base su Citrix è abbastanza semplice. Fornisce un modo per dare ai client su una rete interna un percorso protetto alle risorse su Internet. Consente anche all'amministratore di rete di mantenere un livello di controllo sulla rete.

Se si sta eseguendo l'implementazione presso la sede di un cliente, si consiglia di aggiungere un firewall alla configurazione per proteggere ulteriormente le risorse.
