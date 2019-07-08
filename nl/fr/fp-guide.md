---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: proxy, traffic, appliance

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

# Configuration de la redirection du trafic à proxy direct à l'aide du dispositif Citrix NetScaler VPX
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

Ce guide fournit des informations détaillées sur la procédure de configuration d'un proxy direct (forward proxy) à l'aide du dispositif Citrix NetScaler VPX. Cette configuration a été testée sur un dispositif Citrix NetScaler VPX exécutant une version logicielle 11.1 (édition platine) et des performances de 10 Mbits/seconde.

<img src="images/fp1.png" alt="dessin" style="width: 600px;"/>

## Ce que vous allez faire
{: #what-you-ll-accomplish}

Dans ce guide pas à pas, vous apprendrez à configurer le service :

Tâche  | Description
------------- | -------------
[Commander Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) | Commencez par commander un dispositif Citrix NetScaler VPX.
[Demander un sous-réseau privé](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) | Demandez un sous-réseau privé auprès du support IBM© pour votre compte.
[Activer la redirection vers un cache et l'équilibrage de charge](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) | Identifiez les ressources de votre application, par exemple, les pools d'origines et les mécanismes de diagnostic d'intégrité.
[Configurer le serveur virtuel DNS](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) | Ajoutez vos résolveurs DNS, définissez le groupe de services DNS et configurez votre serveur virtuel DNS.
[Configurer la redirection du trafic HTTP(S) vers un cache](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic) | Configurez la redirection vers un cache de votre serveur virtuel à proxy direct avec trafic HTTP ou HTTPS.
[Configurer la redirection vers un cache pour le trafic SSL (en option)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) | Configurez la redirection vers un cache de votre serveur virtuel à proxy direct en utilisant le trafic SSL et non le protocole HTTP ou HTTPS.
[Configurer la conversion NAT source pour le trafic sortant](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) | Utilisez votre dispositif Citrix NetScaler VPX pour procéder à la conversion NAT source sur le trafic sortant à partir de vos machines client.
[Mettre à jour les paramètres proxy sur le navigateur Internet de la machine client (en option)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) | Mettez à jour vos paramètres proxy au moyen du navigateur Internet de la machine client, si vous le souhaitez.
