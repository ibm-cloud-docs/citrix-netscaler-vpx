---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-6"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Distribuzione predefinita

Quando visualizzi il tuo NetScaler in **Devices > Device List** nel [Portale del cliente![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/), puoi notare che ha un aspetto diverso da quello degli altri server. Specificamente, il dispositivo ha un indirizzo IP privato ma non ha un indirizzo IP pubblico.

La distribuzione predefinita di un NetScaler su {{site.data.keyword.BluSoftlayer_notm}} è progettata per essere quanto più sicura possibile, assegnando automaticamente un indirizzo IP privato come NSIP (NetScaler IP) utilizzato per fini gestionali. Se fai clic sulla freccia a sinistra del NetScaler, la riga viene espansa per mostrare il nome utente predefinito (root) e la password dell'utente root mascherata. 

{{site.data.keyword.BluSoftlayer_notm}} gestisce molte delle decisioni per tuo conto, durante il provisioning. Gestisce, ad esempio, quali indirizzi IP utilizzare e per quali scopi. Chiede quali VLAN vuoi utilizzare per la distribuzione. Automatizza inoltre la maggior parte della configurazione di back-end utilizzando gli script e una API, come ad esempio l'assegnazione di interfacce a VLAN pubbliche e private separate e l'assegnazione dei corretti indirizzi IP a ciascuna interfaccia, compresi NSIP, VIP e SNIP.

## Cosa devo configurare?

Per impostazione predefinita, il NSIP è l'indirizzo IP privato assegnato durante il provisioning, che è l'indirizzo IP che utilizzi per stabilire una connessione al NetScaler per scopi gestionali. Gli SNIP (SubNet IP Address), per impostazione predefinita, sono assegnati dalle stesse sottoreti IP principali che si trovano sulle VLAN da te scelte durante il processo di ordinazione. 

Se hai scelto le stesse VLAN dove si trovano i server con il carico bilanciato da te previsti, non è necessaria alcuna configurazione supplementare di tali SNIP. Per impostazione predefinita, il DNS è impostato sui server dei nomi di {{site.data.keyword.BluSoftlayer_notm}}. In un'implementazione di base, se {{site.data.keyword.BluSoftlayer_notm}} ospita i record DNS per i tuoi server, non è necessaria alcuna ulteriore configurazione.
