---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Distribuzione e configurazione di IBM Hardware Security Module (HSM) con Citrix Netscaler VPX
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

Questa procedura passo dopo passo ti guida nel processo di integrazione di HSM con Citrix Netscaler VPX. I due servizi saranno quindi in grado di comunicare e generare il materiale crittografico necessario per creare un certificato.

## Informazioni sulla distribuzione
{: #about-the-deployment}
Questa distribuzione è stata creata e verificata con le seguenti specifiche del componente:

| Versione & Build NetScaler VPX	| Versione Software HSM | Versione Firmware HSM | Versione Client HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

Se disponi di una versione precedente di VPX oppure se al momento dell'ordine del dispositivo tramite la piattaforma IBM© Cloud vedi solo le versioni 11.1 e precedenti come opzioni di selezione, puoi eseguire l'upgrade del dispositivo in modo che la configurazione descritta in questa guida possa essere completata.
{: note}

## Topologia logica
{: #logical-topology}
Il diagramma riportato di seguito mostra il flusso del traffico di rete per il caso di utilizzo SSL Offload. Fornisce una prospettiva visiva e logica del Trust Link e la configurazione tra VPX e l'applicazione HSM.

<img src="images/network-flows-logical-topology.jpg" alt="immagine" style="width: 700px;"/>

Se non hai familiarità con SSL Offload, consulta questo [articolo Citrix](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html).

## Quali operazioni eseguirai

{: #what-you-ll-accomplish}

In questa guida passo dopo passo, apprenderai come distribuire e configurare un HSM con un Citrix Netscaler VPX:

Attività  | Descrizione
------------- | -------------
[Ordinazione di un HSM (Hardware Security Module)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) | Innanzitutto, dovrai ordinare un HSM.
[Ordinazione di un Citrix Netscaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) | Se non l'hai già fatto, dovrai ordinare un Citrix Netscaler VPX.
[Inizializzazione di HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) | La maggior parte delle configurazioni richiede l'inizializzazione del dispositivo HSM. Senza eseguire tale operazione, possono essere eseguiti solo determinati comandi `show`.
[Creazione di una partizione](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition) | Una partizione è uno spazio logico e indipendente associato o collegato al client che sta richiedendo o creando oggetti crittografici nel motore HSM.
[Installazione del software client HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software) | In questa sottosezione, VPX verrà installato con il software e i programmi di utilità richiesti per interagire con HSM. |
[Come stabilire NTL (Network Trust Link)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) | Un NTL (Network Trust Link) è un canale sicuro utilizzato da HSM (Hardware Security Module) e dal client per comunicare. |
[Creazione di chiavi e generazione di CSR (Certificate Signing Request)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) | In questa sottosezione creerai una coppia di chiavi che verrà utilizzata per generare un CSR (Certificate Signing Request) e per ordinare/richiedere un certificato con esso. |
[Ordinazione del certificato](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) | Ordina un certificato SSL per il tuo Citrix Netscaler VPX.
[Recupero e trasferimento del certificato](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) | Recupera il certificato SSL ordinato in precedenza e tieni pronti tutti i dati per la sua installazione e configurazione nella procedura passo dopo passo successiva.
