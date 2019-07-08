---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: default, deployment, configure, configuration

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Déploiement par défaut d'un Citrix NetScaler VPX
{: #citrix-netscaler-vpx-default-deployment}

En examinant votre NetScaler dans **Unités > Liste d'unités** sur le [portail client ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/), vous remarquerez qu'il se présente différemment des autres serveurs. Il a notamment une adresse IP privée, mais pas d'adresse IP publique.

Sur {{site.data.keyword.BluSoftlayer_notm}}, le déploiement par défaut d'un NetScaler est prévu pour être aussi sûr que possible. A cet effet, une adresse IP privée est automatiquement attribuée comme NSIP (NetScaler IP) pour les besoins de gestion. Si vous cliquez sur la flèche à gauche du NetScaler, la ligne s'étend pour révéler le nom d'utilisateur par défaut (root) et le mot de passe associé (masqué).

Au cours de la mise à disposition, {{site.data.keyword.BluSoftlayer_notm}} prend beaucoup de décisions pour vous. Il choisit, par exemple, les adresses IP à utiliser pour tel ou tel besoin. Il demande quels réseaux locaux virtuels (VLAN) vous souhaitez utiliser pour le déploiement. Il automatise également une grande part de la configuration d'arrière-plan au moyen de scripts et d'une API. Il affecte notamment des interfaces aux VLAN publics et privés séparés et attribue les adresses IP appropriées à chacune d'elles, en particulier l'adresse NSIP et les adresses VIP et SNIP.

## Que dois-je configurer ?
{: #what-do-i-need-to-configure-}

Par défaut, la NSIP est l'adresse IP privée attribuée au cours de la mise à disposition. C'est aussi l'adresse IP que vous utilisez pour vous connecter au NetScaler pour les tâches de gestion. Par défaut, les SNIP (SubNet IP, ou adresses IP de sous-réseau) sont attribuées à partir des mêmes sous-réseaux IP primaires qui se trouvent dans les VLAN que vous choisissez au moment de passer commande.

Si vous avez choisi les mêmes VLAN que ceux où résident vos serveurs à équilibrage de charge, aucune configuration supplémentaire de ces SNIP n'est nécessaire. Par défaut, les serveurs de noms d'{{site.data.keyword.BluSoftlayer_notm}} sont utilisés comme DNS. Dans une implémentation de base, si {{site.data.keyword.BluSoftlayer_notm}} héberge les enregistrements DNS pour vos serveurs, vous n'avez rien d'autre à configurer.
