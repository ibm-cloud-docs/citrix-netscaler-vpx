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

# Configuration d'un VPN IPsec de site à site dans Citrix NetScaler VPX avec le dispositif IBM Virtual Router Appliance 
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

Ce guide fournit des instructions détaillées pour configurer une connexion de site à site de VPN IPSec dans Citrix VPX. Un dispositif IBM Virtual Router Appliance (VRA) est utilisé en tant qu'homologue VPN. 

<img src="images/ipsec1.png" alt="dessin" style="width: 600px;"/>

## A propos du déploiement
Ce déploiement a été conçu et testé dans l'environnement ci-dessous :

| Version & génération de NetScaler VPX 	| Version & description du VRA  | 
| ------------- | ------------- | 
| NS12.1: Génération	48.13.nc | AT&T vRouter 5600 1801q |

Vous devez disposer d’une licence VPX Platinum pour configurer le VPN IPSec.
{: note}

## Avant de commencer

Ce guide part du principe que vous êtes propriétaire des deux appareils. Veuillez consulter les liens suivants pour obtenir des instructions sur la commande. 

-	[Initiation au dispositif logiciel Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[Initiation à IBM Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## Ce que vous allez faire

Dans ce guide, vous allez apprendre à configurer un VPN IPSec dans le périphérique Citrix VPX.

Tâche  | Description
------------- | -------------
[Activer les fonctionnalités requises dans VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) | Tout d'abord, activez les fonctionnalités requises pour créer le VPN IPSec.
[Créer un profil IPSec](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile) |Le profil IPSec comprend des paramètres de sécurité pour l'établissement de la connexion. 
[Créer un tunnel IP](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) | Dans cette section, nous créons un objet tunnel IP pour spécifier les adresses IP locales et distantes, ainsi que les paramètres de protocole.
[Créer un routage PBR (Policy Based Routing)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing) | Le routage PBR est utilisé pour définir les paramètres de trafic uniques pour les sous-réseaux locaux et distants.
[Configurer VRA](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra) | Configurez le dispositif Virtual Router Appliance en utilisant une syntaxe de configuration de VPN équivalente.
[Vérifier le statut VPN](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection) | Vérifiez l'état de fonctionnement du VPN et effectuez un test de connectivité simple.

## Ressources supplémentaires
Les ressources supplémentaires suivantes peuvent vous aider à en savoir plus sur Citrix VPX et Virtual Router Appliance. 

* [CloudBridge Connector ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configuration d'un tunnel CloudBridge Connector entre un dispositif Citrix ADC et un périphérique Cisco IOS ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Documentation Citrix VPX/ADC 12.1![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [Documentation VRA supplémentaire](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
