---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, configure, tune, tuning, ssl, offload

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

# Configuration et optimisation du déchargement SSL avec Citrix NetScaler VPX
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

Cet exemple pas à pas vous guide tout au long du processus de configuration et d'optimisation du déchargement SSL dans Citrix NetScaler VPX. Pour ce faire, vous utiliserez le certificat et le matériel cryptographique générés via le lien HSM.

Ce document suppose que vous avez terminé les étapes de la rubrique [Déploiement et configuration du module IBM© HSM avec Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) pour commander et créer votre paire VPX/HSM.
{: note}

## A propos du déploiement
{: #about-the-deployment}
Ce déploiement a été conçu et testé dans l'environnement ci-dessous :

| NetScaler VPX Version & Build	| Version logicielle HSM | Version microprogramme HSM | Version client HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## Topologie logique
{: #logical-topology}

Le diagramme ci-dessous indique le flux de trafic réseau pour le cas d'utilisation de déchargement SSL. Celui-ci offre une perspective visuelle et logique du lien de confiance et de la configuration qui existent entre Citrix VPX et le dispositif HSM.

<img src="images/network-flows-logical-topology.jpg" alt="dessin" style="width: 700px;"/>

Si vous n'êtes pas familiarisé avec le déchargement SSL, lisez cet [article Citrix ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}.

## Ce que vous allez faire
{: #what-you-ll-accomplish}

Dans ce guide pas à pas, vous allez apprendre à configurer SSL pour Citrix NetScaler VPX :

Tâche  | Description
------------- | -------------
[Installer le certificat](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) | Installez le certificat SSL que vous créé dans l'exemple [pas à pas](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) précédent.
[Vérifier et configurer l'enregistrement DNS](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | Vérifiez qu'un enregistrement DNS existe pour le nom de domaine complet qui pointe vers l'adresse publique à configurer dans Citrix Netscaler VPX comme un serveur virtuel.
[Ajouter et configurer le serveur virtuel SSL](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | Ajoutez et configurez un serveur virtuel SSL.
[Créer et appliquer une nouvelle suite de chiffrement](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | Créez une suite de chiffrement qui donne la priorité aux chiffrements AEAD, ECDHE et ECDSA.

## Ressources supplémentaires
{: #additional-resources}
Les ressources supplémentaires suivantes peuvent vous aider à tirer le meilleur parti de Citrix NetScaler VPX lorsque vous utilisez le module IBM HSM (Hardware Security Module).

* [NetScaler 12.1 Product Documentation (en anglais)![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Gemalto Support Portal (en anglais)![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [Support IBM Cloud](/docs/get-support?topic=get-support-using-avatar){:new_window}
