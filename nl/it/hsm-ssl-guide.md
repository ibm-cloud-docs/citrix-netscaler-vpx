---

copyright:
  years: 2018
lastupdated: "2018-11-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configurazione e ottimizzazione di SSL Offload con Citrix Netscaler VPX
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

Questa procedura passo dopo passo ti guida nella configurazione e ottimizzazione di SSL Offload in Citrix Netscaler VPX, tale procedura viene eseguita utilizzando il certificato e il materiale crittografico generato tramite il link HSM.

**NOTA:** questa procedura passo dopo passo presuppone che tu abbia completato i passi presenti in [Distribuzione e configurazione di IBM© Hardware Security Module (HSM) con Citrix Netscaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) per ordinare e creare il tuo accoppiamento VPX/HSM.

## Informazioni sulla distribuzione
Questa distribuzione è stata creata e verificata con le seguenti specifiche del componente:

| Versione & Build NetScaler VPX	| Versione Software HSM | Versione Firmware HSM | Versione Client HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## Topologia logica
Il diagramma riportato di seguito mostra il flusso del traffico di rete per il caso di utilizzo SSL Offload. Fornisce una prospettiva visiva e logica del Trust Link e la configurazione tra Citrix VPX e l'applicazione HSM.

<img src="images/network-flows-logical-topology.jpg" alt="immagine" style="width: 700px;"/>

Se non hai familiarità con SSL Offload, consulta questo [articolo Citrix ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}.

## Quali operazioni eseguirai

In questa guida passo dopo passo, apprenderai come configurare SSL per un Citrix Netscaler VPX:

Attività  | Descrizione
------------- | -------------
[Installazione del certificato](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) | Installa il certificato SSL che hai creato nella procedura [passo dopo passo](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) precedente.
[Controllo e configurazione del record DNS](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | Assicurati che esista un record DNS per l'FQDN che punti all'indirizzo pubblico che deve essere configurato in Citrix Netscaler VPX come un server virtuale.
[Aggiunta e configurazione del server virtuale SSL](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | Aggiungi e configura un server virtuale SSL.
[Creazione e applicazione di una nuova suite di cifratura](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | Crea una suite di cifratura che dia priorità e abbia come preferenza AEAD, ECDHE e ECDSA.

## Risorse aggiuntive
Le risorse aggiuntive riportate di seguito possono aiutarti a ottenere il massimo dal tuo Citrix Netscaler VPX quando utilizzi IBM Hardware Security Module.

* [NetScaler 12.1 Product Documentation ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Gemalto Support Portal ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [Supporto IBM Cloud](https://{DomainName}/docs/get-support?topic=get-support-using-avatar){:new_window}