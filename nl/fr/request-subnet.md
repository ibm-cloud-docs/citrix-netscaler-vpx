---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: subnet, private, request, vip

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Demande d'un sous-réseau privé
{: #request-a-private-subnet}

Dans la plupart des déploiements, le dispositif {{site.data.keyword.vpx_full}} est déployé au sein d'une configuration avec proxy inverse. Toutefois, pour configurer le VPX avec un proxy direct, des adresses IP virtuelles (VIP) sont nécessaires, car la configuration sera effectuée sur un réseau privé et non sur un réseau public.

Vous devez ouvrir un ticket auprès de l'équipe du support IBM© Cloud afin de demander qu'un réseau privé soit ajouté à votre compte pour votre dispositif {{site.data.keyword.vpx_full}}. Au moins deux adresses privées étant nécessaires, la taille de votre sous-réseau privé devra être au moins égale à /29.  
