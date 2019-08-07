---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, dns, security, check, configure

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

# Vérification et configuration de l'enregistrement DNS
{: #check-and-configure-the-dns-record}

Dans cet exemple pas à pas, le service DNS géré par le fournisseur de services Internet IBM© Cloud sert à la gestion de la zone DNS et de ses enregistrements. Dans ce cas, assurez-vous qu'un enregistrement est créé pour le nom de domaine complet qui est utilisé. L'enregistrement doit pointer vers l'adresse publique à configurer dans le serveur virtuel {{site.data.keyword.vpx_full}}.

<img src="images/12-add-record.png" alt="dessin" style="width: 700px;"/>

L'adresse IP publique statique à utiliser avec Citrix VPX peut être obtenue sur le portail client en accédant à **Unités > Liste des unités**, puis en sélectionnant le nom de votre {{site.data.keyword.vpx_full}}.

<img src="images/13-check-ip.png" alt="dessin" style="width: 300px;"/>
