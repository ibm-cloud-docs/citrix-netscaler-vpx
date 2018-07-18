---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Equilibrage de charge global avec Citrix NetScaler VPX

L'équilibrage global de la charge des serveurs (GSLB, Global Server Load Balancing) est un mécanisme qui distribue le trafic à plusieurs serveurs/instances résidant le plus souvent en différents endroits. L'idée est d'avoir un moteur/serveur d'équilibrage global qui reçoive les demandes des clients et les redirige vers tel ou tel endroit, celui-ci étant déterminé par les critères et algorithmes sélectionnés et configurés par l'administrateur. Deux méthodes reconnues peuvent être utilisées à cet effet au sein du réseau {{site.data.keyword.BluSoftlayer_notm}} :

* **CDN : ** (Content Delivery Network) réseau de distribution de contenus et de médias riches tels que vidéos et images. Le contenu est réparti géographiquement sur des noeuds dispersés, garantissant ainsi des temps de latence aussi courts que possible et des débits de transmission au plus haut niveau. Il est généralement mis en oeuvre lorsque seules des portions particulières du contenu doivent être distribuées, par opposition à des sites web entiers ou des applications entières. Ce service est proposé par {{site.data.keyword.BluSoftlayer_notm}}. Plus de lecture à son propos [ici](https://console.bluemix.net/docs/infrastructure/CDN/getting-started.html#getting-started). 
* **NetScaler VPX :** comme dans le cas d'un équilibrage de charge local classique, NetScaler VPX utilise une hiérarchie d'objets similaire pour répartir le trafic et la charge afférente entre plusieurs endroits. Utilisant des recherches globales basées sur DNS, il choisit l'enregistrement qui correspond au lieu ou site sélectionné en fonction de critères préconfigurés par l'administrateur. Cette option/offre sera décrite plus en détail dans les sections à venir.

Notez que d'autres techniques, telles que la redirection HTTP, sont également disponibles pour la distribution de contenus et peuvent être mises en oeuvre avec le Citrix NetScaler VPX. 

## A propos de GSLB sur VPX

La fonctionnalité d'équilibrage global de la charge des serveurs, ou GSLB, est disponible sur NetScaler VPX. Il suffit de l'activer dans son interface graphique ou via la ligne de commande. 

GSLB utilise des composants/objets très similaires à ceux des déploiements d'équilibrage local de la charge, dans lesquels les entités sont définies par un modèle hiérarchique.

GSLB peut être implémenté à différentes fins, parmi lesquelles :

* **Partage/distribution de la charge :** pour répartir efficacement et intelligemment les ressources entre plusieurs endroits.
* **Récupération après sinistre :** procédure utilisée lorsque le site principal ou primaire tombe en panne ou ne peut plus assurer le service. Dans ce cas de figure, un site de remplacement ou de secours peut prendre le relais.
* **Performances et rendement :** procédé consistant à positionner le contenu au plus près des systèmes finaux ou d'une manière qui améliore le service concerné.

Les principaux composants ou entités mis en jeu dans un déploiement GSLB sont les suivants :

* **Serveurs virtuels :** une VIP (Virtual IP) est une adresse IP à laquelle le client envoie une demande. Le NetScaler termine la connexion du client à la VIP, puis il en ouvre une autre avec un serveur configuré dans le service d'équilibrage (local) de la charge. 
* **DNS (Domain Name System) et serveurs de noms :** la résolution des noms dans un déploiement GSLB fonctionne de manière presque identique au système DNS classique. La différence se situe au niveau de la logique et des critères utilisés pour déterminer la ou les adresses résolues. Pour mener à bien cette résolution, GSLB utilise une méthode d'équilibrage de charge préconfigurée. NetScaler peut être configuré pour interagir avec DNS de différentes manières :
	* DNS faisant autorité (ADNS, Authoritative DNS). Les systèmes NetScaler qui utilisent le mode ADNS font autorité pour un domaine particulier et tous les enregistrements associés.
	* Sous-délégation DNS. Cas où un serveur DNS (faisant autorité pour le domaine) délègue la responsabilité d'un sous-domaine à un système NetScaler.
	* Proxy DNS. Configurés dans ce mode, les systèmes NetScaler transfèrent les demandes DNS à un autre serveur (externe) qui se charge de la résolution des noms.
* **Méthode :** la méthode est un algorithme que le serveur virtuel GSLB utilise pour sélectionner le meilleur service GSLB dans la topologie. L'algorithme évalue les aspects performances qui correspondent aux critères de sélection proprement dits. Les méthodes suivantes sont disponibles :
  * Permutation circulaire (Round Robin) : distribue les demandes entrantes aux différents sites/services GSLB à tour de rôle, sans considération de leur charge.
  * Temps aller-retour (RTT, Round Trip Time) : mesure du temps de réponse entre le serveur DNS local du client et les sites (GSLB). Pour recueillir les métriques RTT, NetScaler utilise différents mécanismes tels que demandes/réponses ICMP Echo (PING), UDP et TCP.
  * Proximité statique (Static Proximity) : utilise une base de données d'adresses IP pour établir la proximité entre le serveur DNS local du client et les sites, puis utilise cette information comme critère pour effectuer une sélection.
  * Moindres connexions (Least Connections) : détermine le plus petit nombre de connexions actives sur chaque site/service et utilise cette information comme critère de sélection.
  * Moindres temps de réponse (Least Response Time) : sélectionne le site ayant le moins de connexions actives et le temps de réponse moyen le plus court.
  * Moindre bande passante (Least Bandwidth) : choisit le site dont la bande passante est la moins occupée, donc celui qui a à gérer le moins de trafic (en Mbit/s).
  * Moindres paquets (Least Packets) : sélectionne le service qui a reçu le plus petit nombre de paquets au cours des 14 dernières secondes.
  * Hachage de l'IP source (Source IP Hash) : sélectionne le service en fonction de la valeur hachée de l'adresse IPv4 ou IPv6 du client.
  * Charge personnalisée (Custom Load) : sélectionne un service qui ne prend part à aucune transaction active. Si tous les services intervenant dans l'équilibrage de charge sont occupés avec des transactions actives, le dispositif sélectionne le moins chargé d'entre eux (en termes d'utilisation processeur, de mémoire et de temps de réponse).

* **MEP (Metric Exchange Protocol) :** protocole propriétaire utilisé par les dispositifs NetScaler pour échanger des métriques (charge et réseau) et des informations de persistance entre sites. MEP permet aux différents sites/NetScalers de la topologie GSLB de se tenir mutuellement informés de leur état de santé. Utilisant les critères fixés par l'administrateur, MEP fournit aux sites un moyen de communiquer et de prendre en charge le trafic sur la base des paramètres de sélection précédemment configurés. MEP utilise les ports TCP 3009 et 3011. Lorsqu'il est désactivé, la sélection des méthodes est limitée à celles qui, dans la liste ci-dessus, sont marquées d'un astérisque (*). Toute autre méthode choisie est remplacée par la méthode Round Robin (permutation circulaire).
* **Surveillance (Monitoring) :** le moteur NetScaler évalue périodiquement l'état des services GSLB distants en utilisant soit le protocole MEP, soit des moniteurs explicites liés aux services en question. Les moniteurs s'utilisent exactement comme avec un service d'équilibrage de charge classique. Dans le cas de GSLB, l'ajout de moniteurs aux services locaux n'est pas nécessaire dans la mesure où cette surveillance est généralement contrôlée par MEP. 
* **Persistance :** fonctionnalité optionnelle qui établit une préférence de site pour un domaine particulier. Dans ce cas d'utilisation particulier, le trafic n'est pas équilibré, mais pris en charge par le même centre de données. Cela peut être utile dans certaines applications, telles que le e-commerce, dans lesquelles les données transactionnelles sont propres à chaque site/serveur.
* **Site GSLB :** les sites peuvent être définis comme des centres de données ou des lieux où un système NetScaler est configuré/présent. Chaque site GSLB est géré par un système NetScaler qui est considéré comme “local” à ce site, tous les autres systèmes/sites distants étant vus et traités comme des sites “distants”.
* **Service GSLB :** objet qui représente (et qui est lié à) un serveur virtuel (normal)/VIP. Il est soit local (même site), soit distant.
* **Serveur virtuel GSLB :** un serveur virtuel GSLB est affecté à un ou plusieurs services GSLB qui font généralement partie de sites (GSLB) différents. Le trafic qu'il reçoit voit sa charge équilibrée et répartie entre les sites qui y sont liés. La sélection du site est réalisée en fonction de la méthode et du cas d'utilisation.
* **Domaine GSLB :** représente le domaine ou la zone dont le serveur virtuel GSLB est responsable. 
* **Service ADNS :** service représenté par une combinaison d'adresse IP et de port, à laquelle sont envoyées les demandes DNS ciblant un domaine pour lequel NetScaler fait autorité. Pour obtenir une réponse, NetScaler passe ces demandes au serveur virtuel GSLB qui est lié à ce domaine.
