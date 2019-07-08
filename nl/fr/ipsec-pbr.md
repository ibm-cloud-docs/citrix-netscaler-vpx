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

# Création d'un routage PBR (Policy Based Routing) 
{: #creating-policy-based-routing}

Une stratégie PBR (Policy Based Routing ou routage basé sur des règles) est nécessaire pour spécifier les paramètres de trafic uniques (tels que les sous-réseaux locaux et distants) que la connexion VPN utilise. Pour créer un profil PBR, procédez comme suit : 

1.	Accédez à **Système > Réseau > PBR** et sélectionnez **Ajouter**.
2.	Entrez un **Nom**.
3.	Conservez **Action** comme paramètre par défaut **ALLOW**.
4.	Pour **Next Hop Type**, sélectionnez **IP Tunnel**, puis choisissez le tunnel [créé](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) dans la liste déroulante **IP Tunnel Name**.
5.	Veillez à cocher **Enable PBR**.
6.	Dans la section **Configure IP**, sélectionnez **=** pour la zone **Operation**, pour la source et la destination.
7.	Spécifiez la première et la dernière adresse IP de sous-réseau dans les zones suivantes : 
  *	**Source IP Low**
  *	**Source IP High**
  *	**Destination IP Low**
  *	**Destination IP High**
8.	Cliquez sur **Create**.

    <img src="images/ipseCreatePBR1.png" alt="dessin" style="width: 200px;"/>

9.	Dans **System > Network > PBRs**, sélectionnez le nouveau routage PBR, cliquez dans la liste **Select Action**, puis sélectionnez **Apply**.

    <img src="images/ipsecCreatePBR2.png" alt="dessin" style="width: 600px;"/>

Pour créer le profil PBR dans la CLI, utilisez la syntaxe suivante : 

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs
  
  ```
  {: codeblock}

  Sachez que toute instance de serveur virtuel ou infrastructure destinée à passer par le tunnel VPN et à se placer derrière le VPX doit être configurée pour utiliser VPX en tant que passerelle par défaut ou pour utiliser une route statique. Cette opération envoie le trafic au VPX lorsque la destination est le sous-réseau distant (homologue). Voir l'exemple de route statique (**10.115.0.0/16**) ci-dessous.
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
