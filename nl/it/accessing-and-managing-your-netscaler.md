---
copyright:
  years: 1994, 2019

lastupdated: "2019-06-11"

keywords: manage, managing, locating, details, portal, device, list

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Gestione del tuo Citrix NetScaler VPX
{: #managing-your-citrix-netscaler-vpx}

I dispositivi Citrix NetScaler sono potenti strumenti con una gamma di funzioni che aiutano a migliorare e perfezionare la soluzione {{site.data.keyword.cloud}} in tantissimi modi. Puoi trovare le informazioni del dispositivo nel portale del cliente dell'infrastruttura {{site.data.keyword.cloud_notm}}, nonché connetterti al dispositivo e configurarne le funzioni.  

## Individuazione dei dettagli di NetScaler nel portale del cliente
{: #locating-netscaler-details-in-the-customer-portal}

I dispositivi Citrix NetScaler sono elencati nell'elenco dispositivi (Device List), come qualsiasi altro server che hai nella piattaforma {{site.data.keyword.cloud_notm}}.

Per trovare l'elenco dispositivi (Device List):

1. Dal tuo browser, apri il [Portale del cliente ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){: new_window} e accedi al tuo account.
2. Nella navigazione del portale del cliente, seleziona **Devices > Device List**.

Vedrai i tuoi dispositivi, ordinati in base al nome. I dispositivi Citrix NetScaler VPX hanno "NetScaler" come tipo dispositivo (Device Type).

Sul lato sinistro della riga per il tuo NetScaler, fai clic sulla freccia per espandere la riga e visualizzare il nome utente e la password mascherata per l'accesso di gestione NetScaler.

Altri dettagli elencati nell'elenco dispositivi (Device List) includono:

* Ubicazione (data center in cui si trova il NetScaler)
* Indirizzo IP privato (che viene utilizzato per stabilire una connessione al NetScaler per le funzioni di gestione)
* Data di inizio (quando la macchina è stata ordinata e fornita)

L'indirizzo IP privato del NetScaler è elencato nel portale, l'indirizzo IP pubblico del NetScaler invece no. Ciò è dovuto al fatto che la gestione del NetScaler viene eseguita utilizzando l'indirizzo IP privato e gli indirizzi IP pubblici per i dispositivi NetScaler vengono utilizzati come VIP (o Virtual IP) del dispositivo, che vengono utilizzati per i servizi di bilanciamento del carico.
{: note}

## Schermata Device Details (Dettagli dispositivo)
{: #the-device-details-screen}

Quando fai clic sul nome di NetScaler si apre la pagina **Device Details** per il NetScaler, che mostra la VLAN sulla quale il tuo NetScaler era stato distribuito, nonché i tuoi indirizzi IP pubblici per il NetScaler. Questi indirizzi IP non possono essere utilizzati per la gestione perché sono gli indirizzi VIP pubblici predefiniti di NetScaler. Li utilizzerai in seguito per eseguire l'associazione a un servizio di bilanciamento del carico.

## Connessione a NetScaler
{: #connecting-to-the-netscaler}

{{site.data.keyword.cloud_notm}} concede un pieno accesso root al tuo dispositivo NetScaler. Per accedere all'IU di gestione di NetScaler, devi essere connesso alla rete privata {{site.data.keyword.cloud_notm}} (utilizzando la VPN di gestione {{site.data.keyword.BluSoftlayer_notm}} oppure eseguendo le funzioni di gestione da una sessione remota su un server all'interno dell'ambiente {{site.data.keyword.cloud_notm}}).

Per stabilire una connessione dal portale del cliente all'IU di gestione di NetScaler, fai clic sul menu a discesa **Actions** nell'angolo superiore destro della schermata **Device Details** e seleziona **Manage Device** per avviare una nuova scheda o finestra a comparsa nel tuo browser. In questo modo verrai instradato al NSIP di NetScaler (l'indirizzo IP privato che avevi visto in precedenza). La pagina che viene visualizzata ti chiederà il nome utente root e la password per il dispositivo. Dopo che avrai immesso queste informazioni, si aprirà la GUI di gestione di NetScaler.

In alternativa, puoi copiare e incollare l'IP privato del dispositivo NetScaler in un browser web.

### Accesso SSH a NetScaler
{: #netscaler-ssh-access}

Puoi anche connetterti al dispositivo NetScaler direttamente utilizzando il tuo client SSH preferito. Usa l'IP privato e le informazioni di accesso per il dispositivo NetScaler dalla pagina Device List e assicurati di essere connesso alla VPN {{site.data.keyword.cloud_notm}}.
