---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Terminologie

La plateforme Citrix NetScaler utilise à la fois une terminologie qui lui est propre et la terminologie et
les concepts des équilibreurs de charge.
 

### IP NetScaler (NSIP)

L'IP de l'équilibreur de charge désignée pour les besoins de gestion.

### SubNet IP (SNIP)

Une SNIP (abréviation de SubNet IP) est l'adresse IP source d'un paquet utilisé par le NetScaler chaque fois qu'il veut communiquer avec un serveur (ou un objet).
Les serveurs utilisent aussi la SubNet IP pour répondre au NetScaler.

### IP virtuelle (VIP)

Aussi appelée VIP (abréviation de Virtual IP), c'est une adresse IP à laquelle un client envoie ses
demandes.
Le NetScaler termine la connexion du client à la VIP, puis il en ouvre une autre avec un serveur configuré dans
le service d'équilibrage de charge.
Il peut s'agir d'une adresse IP publique dans le cas d'un trafic public (Internet) ou d'une adresse IP privée dans le cas
d'un trafic sur réseau privé (intranet).


### Serveur virtuel

Dans la terminologie des équilibreurs de charge, on appelle serveur virtuel l'association
de l'adresse IP, du numéro de port et du protocole à laquelle un client IP se connecte et où
les demandes de trafic sont envoyées pour une application particulière dont la charge est équilibrée par le
NetScaler.


### Service

C'est la combinaison de l'adresse IP, du numéro de port et du protocole utilisés pour router les
demandes vers un serveur spécifique.
Une fois configuré, le service doit être associé à un serveur virtuel. 

### Objet serveur

Entité virtuelle qui vous permet d'attribuer un nom significatif à un serveur physique plutôt que d'utiliser son adresse IP normale.


### Moniteur

Elément qui permet de suivre un service pour s'assurer qu'il fonctionne correctement. Le moniteur
utilise des sondes et des signaux de présence (pulsations, ou heartbeat) pour suivre l'état du service.
