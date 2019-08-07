---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: proxy, update

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

# Mise à jour des paramètres de proxy sur le navigateur Internet de la machine client (en option)
{: #update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-}

Pour mettre à jour vos paramètres de proxy à l'aide du navigateur Internet de la machine client, procédez comme suit :

1. Sélectionnez **Options Internet** dans vos paramètres de navigateur et configurez-les de manière à utiliser un serveur proxy pour les demandes sortantes.
2. Utilisez l'adresse IP de votre serveur virtuel de redirection de cache que vous avez précédemment défini comme étant votre proxy.

Ces paramètres de proxy peuvent ne pas être nécessaires si le dispositif {{site.data.keyword.vpx_full}} est installé au niveau de la couche 3, entre les machines client et Internet.
{: note}

<img src="images/fp17.png" alt="dessin" style="width: 500px;"/>
