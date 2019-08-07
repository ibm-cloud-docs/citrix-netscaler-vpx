---

copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: about, vpx, features, overview

subcollection: citrix-netscaler-vpx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# A propos de {{site.data.keyword.vpx_full}}
{: #about-citrix-netscaler-vpx}

Le {{site.data.keyword.vpx_full}} est un dispositif (appliance) logiciel virtuel dédié qui assure un équilibrage de charge sur le réseau IBM© Cloud public et privé.

Le déploiement d'un {{site.data.keyword.vpx_full}} dans votre solution {{site.data.keyword.BluSoftlayer_notm}} accélère la mise à disposition des applications Web, améliore les performances et offre la garantie que vos applications et services cloud seront toujours optimisés, disponibles et sûrs. Si vous avez des charges de travail importantes (jeux en ligne, Big Data, analytique, etc.) ou des clouds privés, le {{site.data.keyword.vpx_full}} peut vous aider à fournir votre solution aux utilisateurs où et quand ils en ont le plus besoin.

## Caractéristiques et fonctionnalités
{: #features}

* Seul produit capable d'équilibrer la charge du trafic à la fois sur le réseau public et un réseau privé
* Gestion par interface graphique (GUI) ou ligne de commande (CLI)
* De nombreux types de distribution de trafic, notamment :
  * Connexions minimum
  * Permutation circulaire (Round Robin)
  * Moindre temps de réponse
  * Moindre bande passante
  * Moindres paquets
  * Hachage d'URL
  * Hachage de nom de domaine
  * Hachage de l'adresse IP source
  * Hachage de l'adresse IP cible
  * Hachage des adresses IP source/cible
  * Jeton
  * LRTM

* Accélération/déchargement SSL
* Equilibrage de charge de serveur global (GSLB)
  * Utilise l'infrastructure DNS pour connecter le client au meilleur centre de données
  * Surveille la charge et la disponibilité des centres de données pour faire le meilleur choix de connexions
* Commutation de contenu
* Redirection vers un cache (CR, Cache Redirection)
* Capacités de pare-feu applicatif
* Fonctionnalités de sécurité des applications
* Dispositif (appliance) virtuel fonctionnant sur un matériel dédié
* Déployé comme tout autre serveur {{site.data.keyword.BluSoftlayer_notm}}, avec la souplesse et la disponibilité en ligne de mire
* Disponible en plusieurs largeurs de bande : 10 Mbit/s, 200 Mbit/s et 1000 Mbit/s

Le {{site.data.keyword.vpx_full}} peut être déployé à la demande, en seulement 15 minutes, dans n'importe quel centre de données {{site.data.keyword.BluSoftlayer_notm}} de la planète. Plusieurs modèles de licences couvrent une variété de besoins en matière de vitesse et de fonctionnalités et offrent la souplesse qu'exigent les solutions cloud d'aujourd'hui. Cette souplesse garantit une adaptation optimale à tous les cas d'utilisation, de la PME à la grande entreprise.

{{site.data.keyword.BluSoftlayer_notm}} offre le dispositif (appliance) virtuel NetScaler VPX avec un accès root complet et illimité.   

## Sécurité des applications
{: #application-security}

Pour sécuriser le trafic de leurs applications, les clients peuvent tirer parti de fonctionnalités de sécurité, telles que Application Content Filtering (filtrage de contenu), Priority Queuing (mise en file d'attente par priorité) et un pare-feu applicatif (Web Application Firewall).

## Filtrage du trafic
{: #traffic-filtering}

Le {{site.data.keyword.vpx_full}} filtre les demandes des utilisateurs finaux aux serveurs et les réponses des serveurs aux utilisateurs finaux. Une fonctionnalité d'apprentissage intégrée au pare-feu applicatif permet de profiler les sessions en temps réel et de déterminer s'il faut ou non autoriser le trafic.

## Rapports PCI-DSS
{: #pci-dss-reporting}

PCI-DSS est une norme de sécurisation des données de cartes de paiement. Elle consiste en douze critères auxquels les sociétés et organismes amenés à traiter des paiements en ligne par carte bancaire doivent répondre. Le rapport PCI-DSS se compose de la liste des critères pertinents pour votre configuration de pare-feu applicatif. Il indique aussi si, dans son état actuel, votre configuration répond à chaque critère et suggère des solutions pour configurer le pare-feu applicatif de sorte qu'il remplisse toutes les conditions.

## Équilibrage de charge global (GSLB)
{: #global-load-balancing-gslb-}

Avec la fonctionnalité GSLB, l'édition Platinum de NetScaler étend l'équilibreur de charge au-delà des frontières locales du centre de données.

## Extension de votre centre de données
{: #extend-your-datacenter}

Dans l'édition Platinum de NetScaler, la fonctionnalité CloudBridge Connector vous offre un moyen simple d'étendre votre centre de données à {{site.data.keyword.BluSoftlayer_notm}} avec des menus pilotés par des assistants.
