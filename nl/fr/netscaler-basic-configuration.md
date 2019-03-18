---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuration d'équilibrage de charge de base
{: #basic-load-balancing-configuration}

Prenons l'exemple d'une société ayant un site web communautaire (sorte de réseau social rudimentaire) sur lequel les internautes peuvent s'inscrire et obtenir un compte ne demandant pas d'informations sensibles. Avec ce compte, ils peuvent se connecter et poster des photos de leurs animaux domestiques. Il y a en tout trois serveurs web/d'applications et un serveur de base de données en soutien. Le domaine et le DNS sont hébergés par {{site.data.keyword.BluSoftlayer_notm}}, et parce qu'il s'agit d'un petit environnement, le NetScaler et les serveurs web/d'applications siègent tous dans le même réseau local virtuel (VLAN). Cela simplifie les choses, car pour mettre en place une politique d'équilibrage de charge de base, il n'est pas nécessaire de configurer davantage le NetScaler. La procédure suivante est une explication simplifiée à outrance de l'écoulement du trafic dans ce cas de figure :

1. Un utilisateur entre l'URL dans son navigateur.
2. L'enregistrement DNS de l'URL pointe vers l'une des adresses IP virtuelles (VIP) publiques configurées sur le NetScaler.
3. Le NetScaler reçoit le trafic sur cette VIP et prend note du protocole utilisé (en l'occurrence, trafic HTTP sur le port 80).
4. Le NetScaler passe ensuite ce trafic à l'un des serveurs du pool en tenant compte de la méthode d'équilibrage définie (permutation circulaire, persistance de l'IP source, etc.).
5. Le serveur accepte le trafic et l'utilisateur peut alors se connecter.

Pour parvenir à ce résultat, il faudrait normalement configurer le NetScaler de sorte qu'il puisse prendre en charge ce trafic. Mais comme la VIP, l'IP du serveur DNS et la SNIP sont déjà configurées, la configuration s'en trouve simplifiée. 

Dans l'interface utilisateur de NetScaler, sur l'écran Configuration, développez la branche **Traffic Management** (gestion du trafic) à gauche. Développez la sous-section intitulée **Load Balancing** (équilibrage de charge). Effectuez la procédure suivante pour indiquer au NetScaler quels serveurs cible seront inclus dans la politique d'équilibrage de charge :

1. Sous Load Balancing, cliquez sur **Servers**.
2. Cliquez sur **Add**.
3. Entrez le nom du serveur (par exemple, Web1).
4. Entrez l'adresse IP du serveur.
5. Laissez le champ **Traffic Domain** en blanc, car dans ce scénario, vous vous préoccupez seulement du domaine de trafic par défaut.
6. Entrez tout commentaire souhaité à propos de ce serveur.
7. Cliquez sur **Create**.

Répétez cette procédure pour chaque autre serveur du pool.  

**Conseil :** Pour que tous les serveurs d'un même pool soient facilement identifiables, nommez-les en leur appliquant la même convention (par exemple, Web1, Web2, Web3 et ainsi de suite).

Créez ensuite vos services. Vous allez créer un service pour chaque serveur que vous venez d'entrer. Le service est ce qui configure la connexion entre le NetScaler et les serveurs du pool. Chaque service a un nom et spécifie une adresse IP et un port ainsi que le type de données servies.

1. Cliquez sur **Traffic Management > Load Balancing > Services**.
2. Cliquez sur **Add**.
3. Créez un service pour chaque serveur que vous avez créé plus tôt et en utilisant les mêmes informations.

Créez ensuite un serveur virtuel. Le serveur virtuel est une sorte de connexion virtuelle entre l'adresse IP virtuelle (VIP) utilisée pour les serveurs à équilibrage de charge et les services que vous avez créés antérieurement.

1. Cliquez sur **Traffic Management > Load Balancing > Virtual Servers**.
2. Cliquez sur **Add**.
3. Donnez un nom au serveur virtuel.
4. Désignez le protocole dont la charge sera équilibrée (HTTP).
5. Laissez le type d'adresse IP à sa valeur par défaut (soit IP Address). Le champ IP Address est celui dans lequel vous devrez entrer la VIP qui servira de point d'entrée à tous vos utilisateurs.
6. Désignez le port. Par défaut, il s'agit du port 80.
7. Cliquez sur **OK**.

A présent, liez les services que vous avez créés à votre serveur virtuel.

1. Dans l'écran Virtual Servers, cliquez sur le lien **No Load Balancing Virtual Server Service Binding**.
2. Liez chacun des services créés précédemment au serveur virtuel.
3. Cliquez sur **Done**.
4. Cliquez sur le bouton **Refresh**. Les colonnes State et Effective State doivent être au vert.

Vous avez créé un pool et une politique d'équilibrage de charge pour votre site web.

**REMARQUE :**: Pour en apprendre plus sur la configuration du dispositif Citrix NetScaler VPX, visitez la [page de documentation Citrix ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/netscaler.html). Pour une aide supplémentaire, contactez le support et le service commercial {{site.data.keyword.BluSoftlayer_notm}}.
