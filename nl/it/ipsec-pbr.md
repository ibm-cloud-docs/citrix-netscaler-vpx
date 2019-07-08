---

copyright:
  years: 2019
lastupdated: "2019-04-28"

keywords: ipsec, vpn, vpx, tunnel

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

# Creazione di un PBR (Policy Based Routing)
{: #creating-policy-based-routing}

Una politica PBR (Policy Based Routing) è necessaria per specificare i parametri del traffico univoci (ad esempio le sottoreti locale e remota) che saranno utilizzati dalla connessione VPN. Per creare un profilo PBR, utilizza la seguente procedura:

1.	Passa a **System > Network > PBR** e seleziona **Add**.
2.	Immetti il nome (**Name**).
3.	Lascia **Action** con l'impostazione predefinita **ALLOW**.
4.	Per **Next Hop Type**, seleziona **IP Tunnel**, poi seleziona il tunnel [precedentemente creato](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) dall'elenco a discesa **IP Tunnel Name**.
5.	Assicurati di aver selezionato **Enable PBR**.
6.	Nella sezione **Configure IP**, seleziona **=** per il campo **Operation**, sia per l'origine che per la destinazione.
7.	Specifica il primo e l'ultimo IP sottorete nei seguenti campi:
  *	**Source IP Low**
  *	**Source IP High**
  *	**Destination IP Low**
  *	**Destination IP High**
8.	Fai clic su **Create**.

    <img src="images/ipseCreatePBR1.png" alt="immagine" style="width: 200px;"/>

9.	Da **System > Network > PBRs**, seleziona il nuovo PBR, fai clic sull'elenco **Select Action** e quindi scegli **Apply**.

    <img src="images/ipsecCreatePBR2.png" alt="immagine" style="width: 600px;"/>

Per creare il profilo PBR nella CLI, utilizza la seguente sintassi:

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs
  
  ```
  {: codeblock}

  Ti viene comunicato che tutte le istanze del server virtuale o l'infrastruttura pensate per passare tramite il tunnel VPN e posizionarsi davanti al VPX, dovranno essere configurate per utilizzare VPX come gateway predefinito o una rotta statica. In questo modo il traffico sarà inviato al VPX quando la destinazione è la sottorete (peer) remota. Vedi il seguente esempio di rotta statica (**10.115.0.0/16**).
  {: note}

  ```
  >route print
  ===========================================================================
  Interface List
  3...06 93 7a 03 f0 b3 ......XenServer PV Network Device #0
  4...06 ff 8f 6d 89 e8 ......XenServer PV Network Device #1
  1...........................Software Loopback Interface 1
  7...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
  10...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
  ===========================================================================
  
  IPv4 Route Table
  ===========================================================================
  Active Routes:
  Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0    169.54.255.65    169.54.255.73     26
       10.115.0.0      255.255.0.0      192.168.0.1      192.168.0.2     26
  
  ```
  {: codeblock}
