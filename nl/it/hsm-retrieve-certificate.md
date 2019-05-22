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

# Recupero e trasferimento del certificato
{: #retrieve-and-transfer-the-certificate}

Recupera il certificato SSL che hai ordinato in precedenza in modo da essere pronto per la sua installazione e configurazione nella procedura passo dopo passo successiva, [Configurazione e ottimizzazione di SSL Offload con Citrix Netscaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx).

1. Subito dopo la convalida della proprietà del dominio, dovresti ricevere un'email di conferma del completamento dell'adempimento del certificato e del certificato stesso.

	Copia il testo a partire da `---BEGIN CERTIFICATE---` fino a `---END CERTIFICATE---` e salva il contenuto come un nuovo file del certificato con estensione `.cer`.

2. Copia il file del certificato nella directory `/nsconfig/ssl` in Citrix Netscaler VPX.

<img src="images/11-transfer-certificate.png" alt="immagine" style="width: 600px;"/>

Ora Citrix Netscaler VPX è pronto per incorporare il certificato in una distribuzione del bilanciamento del carico utilizzando SSL.