---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: updates, additions, version

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Aggiornamenti recenti per Citrix NetScaler VPX
{: #recent-updates-for-citrix-netscaler-vpx}

## Versione 12.1
{: #version-12-1}

### Server virtuali con più indirizzi IP
{: #virtual-servers-with-multiple-ip-addresses}
Ora puoi creare un singolo server virtuale di bilanciamento del carico con più indirizzi IPv4 e IPv6 VIP non consecutivi/consecutivi. Ogni indirizzo VIP associato a un server virtuale viene gestito come un singolo server virtuale.

Per ulteriori informazioni su questa funzione, vedi l'articolo Citrix [Multiple IP virtual servers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}.

### SSL
{: #ssl}
Per le connessioni SSL sono stati applicati i seguenti aggiornamenti:

* Rimozione delle cifrature deboli dal gruppo cifratura DEFAULT_BACKEND.
* Supporto per le cifrature ECDHE sul frontend di HSM esterno Thales nShield®
* Supporto per le cifrature ECDHE sul frontend di HSM esterno di rete SafeNet
* Rimozione di SSLv2: l'applicazione NetScaler VPX non supporta SSLv2 dalla release 12.1.

Per ulteriori dettagli sugli aggiornamenti SSL 12.1,  consulta [Citrix 12.1 Release Notes ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}.

### Supporto di gruppi di servizi per GSLB
{: #service-groups-support-for-gslb}
Ora puoi configurare i gruppi di servizi basati sull'indirizzo IP, i gruppi di servizi basati sul nome dominio o i gruppi di servizi di ridimensionamento automatico basati sul nome dominio per GSLB. Puoi anche gestire un gruppo di servizi facilmente come un servizio singolo e collegare un gruppo di servizio a un server virtuale, come pure aggiungere servizi al gruppo.

Per ulteriori informazioni sui gruppi di servizi GSLB, vedi l'articolo Citrix [Configuring a GSLB service group ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}.
