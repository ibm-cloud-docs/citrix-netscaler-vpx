---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: proxy, update

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

# Aggiornamento delle impostazioni proxy sul browser Internet della macchina client (Facoltativo)
{: #update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-}

Per aggiornare le tue impostazioni proxy utilizzando il browser internet della tua macchina client, esegui i seguenti passi:

1. Vai a **Internet Options** nelle impostazioni del tuo browser e configuralo per utilizzare un server proxy per le richieste in uscita.
2. Utilizza l'indirizzo IP del tuo server virtuale di reindirizzamento della cache definito nei passi precedenti come tuo proxy.

Queste impostazioni proxy possono non essere necessarie se l'applicazione {{site.data.keyword.vpx_full}} si trova in un percorso di livello 3 di reindirizzamento tra le macchine client e internet.
{: note}

<img src="images/fp17.png" alt="immagine" style="width: 500px;"/>
