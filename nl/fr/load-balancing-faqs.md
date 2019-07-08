---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"

keywords: faq, faqs, questions, vpx, options, ipv6, traffic, network, ha, ssl, vpn

subcollection: citrix-netscaler-vpx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Foire aux questions concernant Citrix NetScaler VPX
{: #faqs-for-citrix-netscaler-vpx}

Voici la liste des questions les plus fréquentes concernant l'utilisation du Citrix NetScaler VPX.

## Qu'est ce qu'un Citrix NetScaler VPX ?
{: faq}

Citrix NetScaler est un ADC (Application Delivery Controller, ou contrôleur de mise à disposition d'applications) qui rend les applications cinq fois meilleures en augmentant leurs performances, en veillant à leur disponibilité et à leur protection et en réduisant considérablement les coûts d'exploitation. Choisissez l'édition de Citrix NetScaler qui répond le mieux aux exigences de vos applications et déployez-la sur les systèmes dédiés convenant à vos besoins de performances. Pour en apprendre plus sur Citrix NetScaler, référez-vous à la [page NetScaler ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){:new_window}
sur le site web Citrix.

## Pourquoi l'équilibrage de charge est-il nécessaire ?
{: faq}

L'équilibrage de charge du trafic est devenu un aspect clé dans de nombreuses implémentations de clients, car il répartit les demandes aux applications et la charge afférente sur plusieurs serveurs. Il confère également un certain nombre d'avantages à la topologie globale, notamment :

* Sécurité. En fonction des protocoles IP et des numéros de port, un isolement logique des serveurs d'applications est créé ou les demandes de trafic sont rejetées.
* Haute disponibilité. Le contenu est répliqué dans un pool ou groupe de serveurs, garantissant aux hôtes sa disponibilité permanente.
* Evolutivité. Davantage de serveurs peuvent être ajoutés à mesure que la demande augmente.
L'équilibreur de charge peut ainsi étendre la répartition de la charge de travail aux serveurs supplémentaires.
* Efficacité. Les charges de travail sont réparties dynamiquement lorsque l'équilibrage de charge est
configuré. Par exemple, des ressources telles que les processeurs peuvent être exploitées plus efficacement.

## Combien d'options d'équilibrage de charge sont-elles disponibles dans {{site.data.keyword.BluSoftlayer_notm}} ?
{: faq}

Pour un comparatif détaillé des offres d'équilibreurs de charge IBM©, voir [Découverte des équilibreurs de charge](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore).

## NetScaler prend-il en charge IPv6 ?
{: faq}

Oui. IPv6 et IPv4 sont tous deux supportés sur le réseau public {{site.data.keyword.BluSoftlayer_notm}}.

## Le NetScaler peut-il équilibrer la charge du trafic sur le réseau privé ?
{: faq}

Oui, d'ailleurs NetScaler est le seul produit d'équilibrage de charge proposé sur {{site.data.keyword.BluSoftlayer_notm}} capable d'étendre son action au réseau privé.

## Le NetScaler peut-il être configuré pour communiquer l'adresse IP source du client à la place de l'IP source du dispositif (appliance) NetScaler ?
{: faq}

Oui, le paramètre **Use Source IP (USIP)** peut être réglé sur **YES** dans l'interface de gestion avancée de NetScaler afin que l'adresse IP source du client soit communiquée à la place de celle du NetScaler.

Le fait d'activer le mode d'adressage USIP sur le dispositif donne à celui-ci un surcroît de souplesse en lui permettant d'utiliser l'adresse IP du client, disponible dans l'en-tête IP, lorsqu'il communique avec le serveur. Lorsque ce mode est activé, le dispositif ouvre les connexions au serveur avec l'adresse IP du client, celle-ci étant également mise à contribution dans la réutilisation des connexions. Ce mode facilite donc une réutilisation limitée par client, en fonction de l'adresse IP du client.

## Dans une configuration haute disponibilité, quels sont les ports utilisés pour l'échange d'informations en lien avec la haute disponibilité entre les noeuds ?
{: faq}

Le port 3010 pour la synchronisation et la propagation des commandes. Le port UDP 3003 pour l'échange des paquets de pulsation (heartbeat, signaux de présence).

## Quelle version de NetScaler VPX inclut-elle la capacité GSLB (Global Server Load Balancing) ?
{: faq}

Platinum.

## Puis-je disposer de NetScaler dans une configuration haute disponibilité ?
{: faq}

Oui, les dispositifs NetScaler VPX prennent en charge les configurations haute disponibilité.

A moins d'être configuré en mode haute disponibilité avec un partenaire, le serveur NetScaler VPX n'est pas redondant. Lorsque vous utilisez NetScaler VPX, il est vivement conseillé de déployer un environnement haute disponibilité dans le cadre de votre stratégie de secours et de récupération.

Il est également important d'assurer la redondance des autres composants matériels et logiciels. Par exemple, les alimentations et les disques locaux ne sont peut-être pas redondants. Toute défaillance de ces équipements peut entraîner la perte de données.

## L'offre NetScaler d'{{site.data.keyword.BluSoftlayer_notm}} inclut-elle la fonctionnalité SSL VPN ?
{: faq}

Oui, cette fonctionnalité, connue sous le nom de NetScaler Gateway™, est incluse dans toutes les éditions.  Pour plus d'informations la concernant, visitez le [site web Citrix ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.citrix.com/products/netscaler-adc/){: new_window}
