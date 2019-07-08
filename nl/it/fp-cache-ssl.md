---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, redirect, ssl, traffic

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

# Configurazione del reindirizzamento della cache per il traffico SSL (Facoltativo)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

Invece di definire il reindirizzamento della cache per il server virtuale con un protocollo HTTP o HTTPS (come discusso del passo precedente), potresti volerlo definire per gestire il traffico SSL.

A tale scopo, segui questi passi:

1. Vai a **Traffic Management > Cache Redirection > Virtual Servers** e fai clic su **Add**. Specifica il nome del server virtuale del proxy di inoltro, seleziona il protocollo SSL e un tipo di cache **FORWARD**. Assegnagli un indirizzo IP dalla tua sottorete privata, con la porta necessaria.

	<img src="images/fp14.png" alt="immagine" style="width: 300px;"/>

	Fai clic su **OK**.

2. Riesamina la pagina di riepilogo e fai clic su **OK** per continuare.
3. Specifica le tue configurazioni per Redirect, DNS Virtual Server e Destination Virtual Server.
4. Fai clic su **Certificate** nel pannello **Advanced Settings** per visualizzare la configurazione correlata al certificato SSL.
5. Fai clic sul campo vuoto **No Server Certificate**.
6. Dall'elenco a discesa Select Server Certificate, seleziona il tuo server SSL.
7. Immetti le informazioni di configurazione del certificato come richiesto.

	<img src="images/fp15.png" alt="immagine" style="width: 400px;"/>

	Fai clic su **Install**.

8. Seleziona **Bind**.

	<img src="images/fp16.png" alt="immagine" style="width: 300px;"/>
