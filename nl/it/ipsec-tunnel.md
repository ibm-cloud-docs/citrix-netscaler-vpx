---

copyright:
  years: 2019
lastupdated: "2019-04-10"

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

# Creazione di un tunnel IP
{: #creating-ip-tunnel}

Devi creare un tunnel IP per specificare non solo gli indirizzi IP locale e remoto, ma anche i parametri del protocollo per la connessione VPN. Per eseguire tale operazione:

1.	Passa a **System > CloudBridge Connector > IP Tunnels**.
2.	Nella scheda **IPv4 Tunnels**, fai clic su **Add**.
3.	Immetti i seguenti parametri:
  *	Name
  *	Remote IP (IP of remote VPN peer)
  *	Remote Mask
4.	Seleziona **Subnet IP** (SNIP) nell'elenco a discesa Local IP.
5.	Scegli lo SNIP appropriato da utilizzare come endpoint VPN dall'elenco a discesa **Local IP**.
6.	Seleziona **IPSEC** come protocollo dall'elenco a discesa.
7.	Scegli il nome del profilo [precedentemente creato](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) dall'elenco a discesa **IPSec Profile Name**. 
8.	Fai clic su **Create**.

    <img src="images/ipsecCreateIPtunnel.png" alt="immagine" style="width: 200px;"/>

Per creare un tunnel IP nella CLI, utilizza la seguente sintassi:
  
  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1
  
  ```
