---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestion de votre Citrix NetScaler VPX
{: #managing-your-citrix-netscaler-vpx}

Les appareils Citrix NetScaler sont de puissants outils armés d'une panoplie de fonctions pour vous aider à améliorer et affiner votre solution {{site.data.keyword.BluSoftlayer_notm}} de différentes manières. Vous trouverez toutes les informations sur l'appareil dans le Portail client, celui-ci vous permettant également de vous y connecter et de configurer ses fonctions.  

## Localiser les détails de NetScaler dans le Portail client

Les appareils Citrix NetScaler, au même titre que les autres serveurs que vous possédez sur la plateforme {{site.data.keyword.BluSoftlayer_notm}}, figurent dans votre Liste d'unités.

Pour trouver la Liste d'unités :

1. Dans votre navigateur, ouvrez le [portail client ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/){: new_window} et connectez-vous à votre compte.
2. Dans la navigation du portail client, sélectionnez **Unités > Liste d'unités**.

Vous obtenez votre liste d'appareils triés par nom. Les appareils Citrix NetScaler VPX sont de type "NetScaler". 

Dans la partie gauche de la ligne consacrée à votre NetScaler, cliquez sur la flèche pour étendre la ligne et révéler le Nom d'utilisateur et le mot de passe associé (masqué), qui permettent d'accéder à l'interface de gestion du NetScaler. 

Les autres détails figurant dans cette liste sont : 

* Emplacement (centre de données dans lequel réside le NetScaler)
* Adresse IP privée (adresse utilisée pour la connexion aux fonctions de gestion du NetScaler)
* Date de début (date à laquelle la machine a été commandée et mise à disposition)

**Remarque :** Tandis que l'adresse IP privée du NetScaler est indiquée dans le portail, son adresse IP publique ne l'est pas. L'adresse IP privée sert en effet à la gestion du NetScaler, alors que les adresses IP publiques sont les VIP (adresses IP virtuelles) utilisées pour les services d'équilibrage de charge.

## L'écran des détails de l'appareil 

En cliquant sur le nom du NetScaler, vous accédez à la page des détails**** le concernant. Cette page indique le VLAN (réseau local virtuel) sur lequel votre NetScaler a été déployé, ainsi que les adresses IP publiques qui vous ont été attribuées sur cet appareil. S'agissant des VIP publiques par défaut du NetScaler, elles ne peuvent pas servir à la gestion de celui-ci. Vous les utiliserez plus tard pour les associer à un service d'équilibrage de charge.

## Connexion à NetScaler

{{site.data.keyword.BluSoftlayer_notm}} vous octroie un accès root complet à votre appareil NetScaler. Pour vous connecter à son interface de gestion, vous devez être préalablement connecté au réseau privé {{site.data.keyword.BluSoftlayer_notm}} (soit vous êtes connecté au VPN de gestion {{site.data.keyword.BluSoftlayer_notm}}, soit vous êtes en train d'exécuter des fonctions de gestion à partir d'une session ouverte à distance sur un serveur au sein de l'environnement {{site.data.keyword.BluSoftlayer_notm}}). 

Pour vous connecter à l'interface de gestion du NetScaler à partir du Portail client, cliquez sur la liste déroulante **Actions**, en haut à droite de l'écran des détails de l'appareil****, et choisissez **Gérer l'unité** pour ouvrir un nouvel onglet ou une nouvelle fenêtre dans votre navigateur. Vous êtes alors connecté à la NSIP (NetScaler IP) de l'appareil, qui n'est autre que l'adresse IP privée que vous avez vue précédemment. La page affichée vous demande le nom d'utilisateur et le mot de passe d'accès root à l'appareil. Une fois ces informations entrées, vous accédez à l'interface graphique de gestion du NetScaler. 

Vous pouvez aussi copier l'adresse IP privée de l'appareil NetScaler et la coller dans un navigateur web.

### Accès SSH au NetScaler

Vous pouvez aussi vous connecter à l'appareil NetScaler directement depuis votre client SSH favori. Pour ce faire, utilisez l'adresse IP privée de l'appareil concerné et les informations de connexion associées, disponibles sur la page Liste d'unités. Assurez-vous également d'être connecté au VPN {{site.data.keyword.BluSoftlayer_notm}}. 
