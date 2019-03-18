---



copyright:
  years: 2017
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configurazione del server virtuale DNS
{: #configure-the-dns-virtual-server}

Per configurare un server virtuale DNS:

1. Vai a Traffic Management > Load Balancing > Servers. 
2. Fai clic su Add per aggiungere due resolver DNS IBM© Softlayer - 10.0.80.11 e 10.0.80.12. 

	<img src="images/fp5.png" alt="immagine" style="width: 200px;"/> <img src="images/fp5b.png" alt="immagine" style="width: 200px;"/>

3. Successivamente, crea e definisci il tuo gruppo di servizi DNS andando a Traffic Management > Load Balancing > Service Groups e selezionando Add. 

	<img src="images/fp6.png" alt="immagine" style="width: 400px;"/> 

4. Seleziona il protocollo DNS, quindi fai clic su OK.

	<img src="images/fp7.png" alt="immagine" style="width: 300px;"/> 
	
5. Nella schermata successiva, aggiungi i nuovi resolver DNS come server dei membri a questo gruppo di servizi facendo innanzitutto clic sul campo vuoto in **Service Group Members**. 

6. Dal pannello Create Service Group Member, specifica la porta DNS 53, quindi fai clic su Create. 

	<img src="images/fp8.png" alt="immagine" style="width: 200px;"/> 
	
7. Fai clic su Close, quindi su Done. 

	Presupponendo che i due resolver DNS IBM Softlayer possano essere raggiunti dalla tua applicazione Citrix NetScaler VPX, il gruppo di servizi verrà mostrato in verde. 

8. Ora, vai a Traffic Management > Load Balancing > Virtual Servers e fai clic su Add per definire il tuo server virtuale DNS.
9. In Basic Settings, assegna un nome al tuo server virtuale, scegli il protocollo DNS e la porta 53, quindi assegna un indirizzo IP dalla tua sottorete privata. 

	<img src="images/fp9.png" alt="immagine" style="width: 300px;"/> 
	
10. Nella pagina successiva, fai clic sul campo vuoto denominato **No Load Balancing virtual Server ServiceGroup Binding**.
11. Seleziona il gruppo di servizi DNS definito precedentemente dall'elenco a discesa e fai clic su Bind.  

	<img src="images/fp10.png" alt="immagine" style="width: 300px;"/> 
	
12. Fai clic su Continue seguito da Done. 

Ora lo stato del tuo server virtuale DNS dovrebbe essere visualizzato in verde. 

<img src="images/fp11.png" alt="immagine" style="width: 500px;"/> 
