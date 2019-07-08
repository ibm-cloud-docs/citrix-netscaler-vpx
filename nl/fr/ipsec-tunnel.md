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

# Création d'un tunnel IP 
{: #creating-ip-tunnel}

Vous devez créer un objet de tunnel IP pour spécifier non seulement les adresses IP locale et distante, mais également les paramètres de protocole de la connexion VPN.  Pour ce faire :

1.	Accédez à **System > CloudBridge Connector > IP Tunnels**.
2.	Dans l'onglet **IPv4 Tunnels**, cliquez sur **Add**.
3.	Entrez les paramètres suivants : 
  *	Name
  *	Remote IP (IP de l'homologue VPN distant)
  *	Remote Mask
4.	Sélectionnez **Subnet IP** (SNIP) dans la liste déroulante des adresses IP locales.
5.	Choisissez l'adresse SNIP appropriée à utiliser comme noeud final de VPN dans la liste déroulante **Local IP**. 
6.	Sélectionnez le protocole **IPSEC** dans la liste déroulante.
7.	Choisissez le nom de profil [créé](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) dans la liste déroulante **IPSec Profile Name**. 
8.	Cliquez sur **Create**.

    <img src="images/ipsecCreateIPtunnel.png" alt="dessin" style="width: 200px;"/>

Pour créer un tunnel IP dans la CLI, utilisez la syntaxe suivante : 
  
  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1
  
  ```
