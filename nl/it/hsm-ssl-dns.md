---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, dns, security, check, configure

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

# Controllo e configurazione del record DNS
{: #check-and-configure-the-dns-record}

In questo esempio passo dopo passo, il servizio DNS di IBM© Cloud Internet Services viene utilizzato per gestire la zona DNS e i relativi record. In questo caso, devi assicurarti che venga creato un record per l'FQDN utilizzato. Il record deve puntare all'indirizzo pubblico che deve essere configurato nel server virtuale Citrix Netscaler VPX.

<img src="images/12-add-record.png" alt="immagine" style="width: 700px;"/>

L'indirizzo IP pubblico statico da utilizzare con Citrix VPX può essere recuperato dal portale del cliente spostandoti in **Devices > Device List** e selezionando il nome del tuo Citrix Netscaler VPX.

<img src="images/13-check-ip.png" alt="immagine" style="width: 300px;"/>
