---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuration de Citrix NetScaler VPX en tant que proxy direct (forward proxy)
{: #setting-up-citrix-netscaler-vpx-as-a-forwarding-proxy}

Le proxy direct (de l'anglais "forward proxy", autrement dit un proxy normal, non inversé) agit comme point unique de contrôle entre les clients situés dans un réseau interne et l'Internet. Il permet à l'administrateur du réseau ou de la sécurité de créer des politiques visant à restreindre l'accès aux sites Internet.

Lorsqu'un client situé dans le réseau interne émet une demande, c'est l'adresse IP du proxy qui est utilisée pour relayer cette demande et l'envoyer au serveur distant, sur l'Internet. Le serveur distant renvoie sa réponse au proxy, qui la retourne au client.

Généralement, un proxy est associé à un pare-feu pour assurer la sécurité des clients dans un réseau interne.

## Etape 1 : demander l'attribution d'adresses VIP utilisables dans le réseau privé 

Lorsqu'un client passe commande d'un équilibreur de charge Citrix NetScaler VPX auprès du portail {{site.data.keyword.BluSoftlayer_notm}}, sa demande est censée porter sur un proxy inverse (reverse proxy). Il lui est demandé d'indiquer le nombre d'adresses IP "publiques" qu'il souhaite utiliser comme adresses IP virtuelles (VIP).

Dans le cas d'un proxy direct (non inversé), les VIP doivent être configurées sur le réseau privé. Un ticket de demande de service doit être ouvert afin de demander la mise en place d'adresses VIP pour le réseau privé. C'est le nombre de VIP requises qui détermine la taille du sous-réseau demandé dans le ticket. Les informations concernant le sous-réseau sont retournées dans le ticket.

Dans notre exemple, nous avons demandé un sous-réseau `/29` et obtenu comme résultats :

* La création du sous-réseau `10.114.27.0/29` à l'usage des VIP privées

* L'attribution de la SNIP (Subnet IP) `10.114.52.101` et du sous-réseau routé `10.114.27.0/29`

* L'ajout, par l'équipe de support, des VIP `10.114.27.0-3` au Citrix NetScaler VPX

## Etape 2 : activer les fonctionnalités d'équilibrage de charge et de redirection vers un cache sur le Citrix NetScaler VPX

Par défaut, les fonctionnalités d'équilibrage de charge et de redirection vers un cache (CR, Cache Redirect) sont désactivées sur l'équilibreur de charge Citrix NetScaler VPX. La commande `enable ns feature cr lb` permet de les activer.


## Etape 3 : créer le proxy direct

Utilisez la ligne de commande pour envoyer les commandes suivantes au Citrix NetScaler VPX. Dans notre scénario, un seul des deux serveurs DNS d'{{site.data.keyword.BluSoftlayer_notm}} est ajouté.  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

La ligne 1 crée le cache cible de la redirection. Le protocole dont le trafic est redirigé est HTTP et `10.114.27.3` est l'une des adresses VIP demandées sur le réseau privé. Le port utilisé est le 80, c'est-à-dire le port par défaut de HTTP, mais comme cette combinaison d'adresse et de port sera utilisée comme instruction de proxy dans le navigateur, il est possible de changer le numéro de port pour une valeur spécifique, si nécessaire.

La ligne 2 ajoute une VIP d'équilibrage de charge qui représentera le “vrai” DNS.

La ligne 3 ajoute l'adresse IP du “vrai” DNS en tant que service. Cette adresse peut être celle du DNS du client ou une adresse renvoyant aux résolveurs DNS fournis par {{site.data.keyword.BluSoftlayer_notm}}.

La ligne 4 lie la VIP au “vrai” serveur. Toutes les demandes de résolution DNS adressées à `10.114.27.4` seront envoyées à `10.0.80.12`.

La ligne 5 indique au serveur virtuel proxy direct d'utiliser le DNS virtuel pour la résolution des noms.

## Configuration du client

Avant d'aborder la personnalisation du client en vue d'utiliser le proxy direct, assurez-vous qu'il n'est pas possible de joindre un site public (par exemple, http://www.ibm.com) à partir d'un navigateur tel que Firefox ouvert sur ce client. Comme il ne doit pas y avoir d'interface publique sur le client, cette demande devrait échouer. 

Dans l'exemple suivant, on configure un client Linux.

Quelques changements doivent être apportés au client. Le premier consiste à faire pointer le résolveur fonctionnant sur le client vers le DNS virtuel. Cela peut être fait de deux manières.

Vous pouvez éditer manuellement le fichier `/etc/resolv.conf` afin de pointer sur l'adresse virtuelle du DNS. Sachez cependant que les outils de gestion du client peuvent inverser ces changements et rétablir les anciens réglages.  

Ou bien vous pouvez éditer l'interface `/etc/sysconfig/network-scripts/ifcfg-ethx` et ajouter l'instruction `DNS1=`. Après quoi, vous pouvez lancer une commande de redémarrage du service réseau afin que ce changement soit pris en compte.

Dans les deux cas, l'adresse IP du DNS devra être configurée en tant qu'adresse de DNS virtuel, et le navigateur du client devra être configuré pour adresser les demandes au proxy direct Citrix NetScaler VPX.

Utilisez les étapes suivantes dans Firefox pour effectuer les changements nécessaires :

1. Cliquez sur **Préférences > Avancé > Réseau > Paramètres de connexion**.

* Sélectionnez **Configuration manuelle du proxy** et entrez les données suivantes :

  * **Adresse :** 10.114.27.3

  * **Port :** 80

  * Cochez la case **Utiliser ce serveur proxy pour tous les protocoles**.

* Cliquez sur **Sauvegarder** et fermez la fenêtre du navigateur.

L'adresse IP `10.114.27.3` est celle du cache cible de la redirection qui a été créé à l'étape 1.

A ce stade, la configuration est complète et vous pouvez accéder à l'Internet public depuis la ressource isolée sur le réseau privé.

## Validation de la configuration

Le client étant maintenant configuré pour utiliser le proxy direct, essayez à nouveau d'accéder à un site public. Cette fois, la demande doit aboutir.

Vous pouvez utiliser les commandes d'affichage suivantes pour vérifier l'état du proxy direct.

**show cr policy :** affiche toutes les politiques de redirection vers un cache existantes.

**show policy map :** affiche les politiques de mappe qui ont été configurées et les informations associées.

**show cr vserver :** affiche un serveur virtuel de redirection vers un cache spécifique ou tous les serveurs virtuels de redirection vers un cache configurés.

**stat cr vserver :** affiche les statistiques des serveurs virtuels de redirection vers un cache.

La configuration d'un proxy direct de base sur Citrix est assez simple. Elle permet aux clients situés dans un réseau interne de disposer d'un moyen d'accès sécurisé aux ressources sur l'Internet. Elle permet aussi à l'administrateur réseau de maintenir un niveau de contrôle du réseau.

En cas d'implémentation sur le site d'un client, il est conseillé d'ajouter un pare-feu à la configuration afin de renforcer la protection des ressources.
