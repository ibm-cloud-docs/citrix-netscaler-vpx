---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, configure, configuration, http, traffic

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

# Configurazione del reindirizzamento della cache per il traffico HTTP(S)
{: #configure-cache-redirection-for-http-traffic}

Per configurare il reindirizzamento della cache per il traffico HTTP o HTTPS, segui i seguenti passi:

1. Vai a **Traffic Management > Cache Redirection > Virtual Servers** e fai clic su **Add**.
2. Specifica il nome del tuo server virtuale del proxy di inoltro. Seleziona il protocollo **HTTP** e il tipo di cache **Forward** dai rispettivi elenchi a discesa. Quindi assegna un indirizzo IP a questo server virtuale dalla tua sottorete privata.

	<img src="images/fp12.png" alt="immagine" style="width: 300px;"/>

	Fai clic su **OK** per continuare.

3. Riesamina la pagina di riepilogo e fai clic su **OK**.  
4. Fai clic su **Traffic Settings** per visualizzare le impostazioni di configurazione aggiuntive.
5. Da Traffic Settings, seleziona una delle tre opzioni di reindirizzamento riportate di seguito, a seconda dei tuoi requisiti:
	* **Cache** - Indirizza tutte le richieste in uscita al tuo pool di server cache locale.
	* **Policy** - Controlla la politica di reindirizzamento della cache per stabilire se la richiesta deve essere inoltrata al pool di server cache o ai server di destinazione (origine).
	* **Origin** – Indirizza tutte le richieste in uscita ai rispettivi server di destinazione (origine).

6. Dall'elenco a discesa **DNS Virtual Server Name**, seleziona il server virtuale DNS configurato precedentemente e imposta l'opzione **Redirect** su **Origin**.

	<img src="images/fp13.png" alt="immagine" style="width: 300px;"/>

	**NOTA:** l'impostazione **Destination Virtual Server** viene utilizzata quando il traffico in uscita deve essere indirizzato al pool di server cache locale. Lasciala vuota quando vuoi indirizzare tutto il traffico in uscita ai server di origine.

7. Fai clic su **OK** seguito da **Done**.
