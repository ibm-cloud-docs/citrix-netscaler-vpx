---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, security, add, configure

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

# Aggiunta e configurazione del server virtuale SSL
{: #add-and-configure-the-ssl-virtual-server}

Per aggiungere e configurare il tuo server virtuale SSL, esegui la seguente procedura:

1. Vai a **System > Settings > Configure Basic Features**. Seleziona **SSL Offloading**, quindi fai clic su **OK**.
2. Nella GUI di NetScaler, vai a **Traffic Management > Load Balancing > Services > Add** e specifica il nome, l'indirizzo IP e imposta il protocollo come **HTTP**. Premi **OK** per terminare.
3. Conferma che il servizio è operativo:

	<img src="images/15-confirm-service.png" alt="immagine" style="width: 700px;"/>

4. Ripeti il passo due per tutti i server aggiuntivi.
5. Passa a **Traffic Management > Load Balancing > Virtual Servers >** e fai clic su **Add**. Specifica il nome e seleziona **SSL** come protocollo, quindi immetti l'indirizzo IP pubblico. Premi **OK** per terminare.
6. Ora seleziona **No Load Balancing Virtual Server Service Binding** e fai clic su **Select**. Seleziona i servizi che hai creato nei passi precedenti e fai clic su Select, quindi fai clic su **Bind/Continue**.

	<img src="images/18-bind-service.png" alt="immagine" style="width: 700px;"/>

7. Infine, fai clic su **No Server Certificate**, quindi fai clic su **Select Server Certificate** e seleziona il certificato che hai installato in precedenza. Fai clic su **Select**, quindi su **Bind/Continue**, poi su **DONE** per terminare.
