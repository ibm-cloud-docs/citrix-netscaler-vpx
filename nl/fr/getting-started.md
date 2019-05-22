---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation au dispositif logiciel Citrix NetScaler VPX
{: #getting-started}

Le déploiement d'un Citrix NetScaler VPX dans votre solution {{site.data.keyword.BluSoftlayer_notm}} accélère la mise à disposition des applications Web, améliore les performances et offre la garantie que vos applications et services cloud seront toujours optimisés, disponibles et sûrs. Si vous avez des charges de travail importantes (jeux en ligne, Big Data, analytique, etc.) ou des clouds privés, le Citrix NetScaler VPX peut vous aider à fournir votre solution aux utilisateurs où et quand ils en ont le plus besoin.

## Avant de commencer
Pour commencer à utiliser Citrix NetScaler VPX, vous devez connaître les informations suivantes :

* Vos informations de connexion au portail client IBM© Cloud
* L'emplacement de déploiement de votre équilibreur de charge
* Le type de Netscaler qui correspond le mieux à vos besoins (pour plus d'informations, voir [Découverte des équilibreurs de charge](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)
* Le nombre d'adresses IP publiques dont vous avez besoin
* Le réseau local virtuel auquel vous voulez affecter l'équilibreur de charge

## Commande d'un Citrix NetScaler VPX

Pour commander un dispositif logiciel Citrix NetScaler VPX, accédez à la page de commande sur le portail client :

1. Dans votre navigateur, ouvrez le [portail client ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/){: new_window} et connectez-vous à votre compte.
2. Dans la navigation du portail client, sélectionnez **Unités > Liste d'unités** et cliquez sur le lien **Commander unités**.
3. Faites défiler la page **Commander les produits et services de SoftLayer**, jusqu'à la section Réseau et cliquez sur le lien **Commander** en dessous de Citrix NetScaler VPX.
4. Dans le menu déroulant, sélectionnez l'emplacement où vous voulez que soit déployé votre dispositif logiciel Citrix NetScaler VPX.  
5. Sélectionnez le type de NetScaler convenant le mieux à vos édition de logiciel, version de logiciel et besoins de traitement.
6. Sélectionnez le nombre d'adresses IP publiques dont vous avez besoin.  
	Il s'agit des adresses IP publiques qui seront déployées en tant que VIP (IP virtuelles) sur votre NetScaler VPX.
7. Cliquez sur **Continuer**.
8. Entrez les informations requises par l'ARIN (ou le RIR équivalent dans votre région de déploiement) pour les adresses IP que vous avez demandées.
9. Entrez vos informations de contact.
10. Sélectionnez votre réseau local virtuel (VLAN).
	Pour minimiser les temps de latence et optimiser l'utilisation de vos ressources réseau, affectez le Citrix NetScaler VPX au même VLAN que celui qui contient les serveurs auxquels le trafic sera distribué.
11. Passez en revue la commande, acceptez les dispositions et cliquez sur **Valider la commande**. Le dispositif logiciel Citrix NetScaler VPX est déployé avec les caractéristiques que vous avez choisies.

## Etapes suivantes

Vous pouvez en apprendre davantage sur les [fonctions](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-about-citrix-netscaler-vpx) de Citrix Netscaler VPX, consulter la [terminologie](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-citrix-netscaler-vpx-terminology) spécifique de Netscaler, ou commencer à [configurer](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-basic-load-balancing-configuration) votre Netscaler.
