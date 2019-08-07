---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: gslb, vpx, cdn, object storage

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Equilibrage de charge global
{: #global-load-balancing}

L'équilibrage global de la charge des serveurs (GSLB) est une méthode de division et de répartition du trafic sur plusieurs serveurs qui utilise la résolution DNS et le lieu géographique comme moyens de déterminer où le trafic serveur doit être envoyé. Généralement, pour limiter autant que possible les temps de latence et préserver les performances, un équilibreur de charge global envoie la demande d'un client au serveur le plus proche de celui-ci.

Vous n'avez peut-être pas besoin de l'implémentation complète d'une solution d'équilibrage de charge global. Celle-ci requiert en effet plusieurs instances d'un équipement adapté et, selon vos besoins, d'autres solutions pourraient être plus attrayantes pour vous. Une solution GSLB reste un bon choix si vous avez besoin d'équilibrer la charge de sites web entiers et d'applications entières. Si vos besoins concernent seulement des parties de votre contenu telles que vidéos, images et autres gros fichiers, un [réseau de distribution de contenus (CDN)](/docs/infrastructure/CDN?topic=CDN-about-content-delivery-networks-cdn-)
sera certainement plus approprié (et plus facile à déployer).

## {{site.data.keyword.vpx_full}}
{: #citrix-netscaler-vpx}

Le {{site.data.keyword.vpx_full}} est le seul équipement configurable par le client qui effectue un vrai équilibrage global de la charge. NetScaler est un dispositif (appliance) multifonction qui peut équilibrer globalement la charge en s'aidant de recherches DNS. Vous pouvez pointer dessus comme un serveur DNS. Il examinera les serveurs dont il doit équilibrer la charge, effectuera un calcul de distance et retournera un enregistrement avec l'IP du serveur le plus proche du client demandeur.

La mise en place d'un équilibrage de charge global nécessite une configuration de dispositif NetScaler dans chaque centre de données. Chaque configuration de dispositif Netscaler peut être constituée d'un unique Netscaler ou d'une paire de Netscaler en mode haute disponibilité, selon vos besoins, et assure l'équilibrage local de la charge des serveurs qu'elle dessert. Tous sont configurés pour dialoguer entre eux et échangent des informations d'état sur chaque serveur affecté à la rotation. Toute demande DNS parvenant à ces dispositifs NetScaler ainsi configurés peut obtenir en retour un enregistrement adéquat, désignant un serveur en ligne et réactif. Un serveur qui ne répond pas est retiré de la rotation et un autre est sélectionné à la place.

Vous devrez déjà avoir un équilibreur de charge configuré, même s'il ne dessert qu'un seul serveur. Il vous faudra des adresses IP supplémentaires pour certains services, notamment l'IP du site GSLB. Cette IP sera utilisée par le NetScaler pour communiquer avec les autres NetScalers dans le protocole d'équilibrage de charge global.

Les procédures d'équilibrage global suivantes utilisent :

### VPX1
{: #vpx1}

`50.97.235.236` est nommée `VPX1Vserver`. Il s'agit de la VIP d'équilibrage de charge local pour cet équipement. `50.23.66.52` sera appelée `VPX1site`. Il s'agit de l'IP locale du GSLB de cet équipement.

### VPX2
{: #vpx2}
`208.43.241.249` est utilisée pour `VPX2Vserver`. L'IP de GSLB correspondante est `208.43.224.4`, qui sera appelée `VPX2site`.

1. Allez dans **Traffic Management > GSLB** et faites un clic droit pour activer la fonctionnalité (option Enable Feature). Ensuite, sélectionnez **Sites** et cliquez sur **Add**.

2. Sur le premier équipement, entrez VPX1 comme nom, choisissez Local comme type et entrez `50.23.66.52` comme adresse IP du site, puis sélectionnez **Close**.

	Le statut du site doit être au vert. N'ajoutez pas encore de site distant.

3. Allez dans **Traffic Management > GSLB** et sélectionnez **GSLB Wizard**. Cliquez sur **Next**. Entrez le nom d'hôte dont la charge sera équilibrée (dans cet exemple, `gslb.tsstesting.com`), conservez A comme type d'enregistrement (Record Type) et ANY comme type de service (Service Type). Le nom du serveur virtuel sera fourni automatiquement. Cliquez sur **Next**.

4. Choisissez la forme d'équilibrage et la méthode de persistance souhaitées, comme vous le feriez pour un équilibrage de charge standard. Cliquez sur **Next**.

5. Le site est déjà prérempli. Vous n'avez donc rien à ajouter. A la place, cliquez sur le '+' vert à côté du nom du premier site. Dans la liste, sélectionnez le serveur virtuel (Vserver) sur cet équipement et cliquez sur **Create**. Le site est normalement configuré avec l'IP de site et l'IP de Vserver de votre configuration d'équilibrage de charge et affiché en vert. Cliquez sur **Next**, **Finish**, puis **Exit**.

6. Effectuez les mêmes actions sur le NetScaler suivant, en utilisant les valeurs pour celui-ci.

7. Sur les deux serveurs, allez dans **Traffic Management > DNS > Records > A records** et examinez la liste. Vous devez voir des entrées `root.servers.net` ainsi que votre nom d'hôte avec le type `GSLB DOMAIN`. 

8. Allez dans **Traffic Management > DNS > Name Servers** et cliquez sur **Add**. Entrez une adresse IP existant sur le NetScaler (par exemple, son IP publique). Cliquez sur **Local** et conservez UDP comme protocole. Cliquez sur **Create**, puis sur **Close**. L'état effectif doit être ENABLED et UP.

9. Allez dans **System > Network > IPs** et ouvrez l'adresse IP GSLB. Assurez-vous que **Management** est sélectionné pour les deux machines.

10. Ensuite, sur les deux serveurs, retournez dans **Traffic Management > GSLB** et déroulez à nouveau l'assistant. Cette fois, cliquez sur **Next** et sélectionnez **Modify Configuration for Existing Domains**. Sélectionnez le nom d'hôte dans la liste et cliquez sur **Next** à deux reprises.

11. Dans le champ d'adresse du site, entrez l'adresse IP du site de l'autre NetScaler et associez-lui le nom de site de cet autre NetScaler, puis cliquez sur **Add**. La ligne du site sera complétée d'une option pour vous permettre de cliquer à nouveau sur le '+' vert. Cliquez sur le signe plus du site distant pour ajouter un autre site. Entrez l'IP de service du serveur virtuel (Vserver) (celle des serveurs dont la charge est équilibrée, et non l'IP du site GSLB) et le port, puis cliquez sur **Create** et **Close**, **Next**, **Finish**, puis **Exit**.

Si tout a fonctionné jusqu'ici et que les deux serveurs sont configurés, tout doit être au vert dans les colonnes d'état ou de statut des serveurs virtuels, services et sites GSLB. Vous remarquerez qu'il y a maintenant deux entrées dans la liste des services GSLB, sur les deux machines, si elles sont synchronisées correctement. A ce stade, les serveurs communiquent entre eux.

Vous devez maintenant configurer DNS.

Dans notre exemple, `gslb.tsstesting.com`, les enregistrements NS et glue seraient à créer dans la zone tsstesting.com :

    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; nameserver IP of first NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; nameserver IP of second NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias to the GSLB object on the NetScaler appliance

N'oubliez pas que vous ne pouvez utiliser des enregistrements CNAME qu'avec des noms d'hôte, et non avec la racine du domaine.

Cette configuration associe aux serveurs de noms utilisés pour les demandes adressées à `gslb.tsstesting.com` les adresses IP des dispositifs NetScaler sur lesquels vous avez configuré DNS. L'enregistrement CNAME traduit `tsstesting.com` en une demande à `gslb.tsstesting.com`. Toute demande adressée à `www.tsstesting.com` ira ensuite au NetScaler pour être résolue et obtiendra en retour un enregistrement tenant compte de la
méthode d'équilibrage de charge que vous avez configurée.

Pour plus d'informations sur la fonction d'équilibrage de charge global de NetScaler, consultez les ressources suivantes :
* [Configuring the Netscaler for global load balancing ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://support.citrix.com/article/CTX110348){: new_window}
* [How DNS(Domain Name System) works with GSLB feature on NetScaler ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://support.citrix.com/article/CTX122619){: new_window}
* [Information on the MEP protocol and site monitoring ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://support.citrix.com/article/CTX111081){: new_window}

Il existe d'autres produits qui peuvent offrir une fonctionnalité similaire pour répartir le trafic en fonction de la géographie :

### CDN
{: #cdn}

Les réseaux de distribution de contenus (CDN, Content Delivery Network) vous permettent de télécharger ou de fournir un contenu d'origine à des serveurs cache géographiquement dispersés (CDN), qui le fournissent ensuite au client demandeur. Les CDN donnent le meilleur d'eux-mêmes avec les contenus statiques et en bloc, tels que les images et les vidéos qui ne changent pas au fil du temps.

Pour plus d'informations sur les CDN, consultez [cette documentation](/docs/infrastructure/CDN?topic=CDN-getting-started).

### Object Storage
{: #object-storage}

Le produit Object Storage d'{{site.data.keyword.BluSoftlayer_notm}} peut être configuré pour fournir les contenus à partir de différents centres de données disséminés en plusieurs endroits. Une application tenant compte de la géographie peut effectuer des recherches de localisation à la demande du client et renvoyer une URL pointant sur le stockage d'objets (Object Storage) le plus proche du client. Object Storage s'accompagne également d'un frontal CDN, si nécessaire, pour fournir des services de cache additionnels, comme indiqué plus haut.

Pour plus d'informations et une introduction à Object Storage, consultez [cette documentation](/docs/services/cloud-object-storage?topic=cloud-object-storage-about).
