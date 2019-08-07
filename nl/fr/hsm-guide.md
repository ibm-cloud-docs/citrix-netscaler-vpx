---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security

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

# Déploiement et configuration du module IBM HSM avec {{site.data.keyword.vpx_full}}
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

Cette rubrique va vous guider tout au long de l'intégration du module HSM à {{site.data.keyword.vpx_full}}. Les deux services seront alors en mesure de communiquer et de générer les données cryptographiques nécessaires à la création d'un certificat.

## A propos du déploiement
{: #about-the-deployment}
Ce déploiement a été conçu et testé dans l'environnement ci-dessous :

| NetScaler VPX Version & Build	| Version logicielle HSM | Version microprogramme HSM | Version client HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

Si vous possédez une ancienne version de VPX ou si, lors de la commande du périphérique via la plateforme IBM© Cloud, seules les versions 11.1 et antérieures sont proposées comme options de sélection, vous pouvez mettre à niveau le dispositif afin d'aller au bout de la configuration décrite dans ce guide.
{: note}

## Topologie logique
{: #logical-topology}
Le diagramme ci-dessous indique le flux de trafic réseau pour le cas d'utilisation de déchargement SSL. Celui-ci offre une perspective visuelle et logique du lien de confiance et de la configuration qui existent entre le VPX et le dispositif HSM.

<img src="images/network-flows-logical-topology.jpg" alt="dessin" style="width: 700px;"/>

Si vous n'êtes pas familiarisé avec le déchargement SSL, lisez cet [article Citrix](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html).

## Ce que vous allez faire

{: #what-you-ll-accomplish}

Dans ce guide, vous apprendrez à déployer et configurer un module HSM avec {{site.data.keyword.vpx_full}} :

Tâche  | Description
------------- | -------------
[Commander un module HSM (Hardware Security Module)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) | Vous allez tout d'abord commander un HSM.
[Commander un dispositif {{site.data.keyword.vpx_full}}](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) | Si ce n'est pas déjà fait, commandez un {{site.data.keyword.vpx_full}}.
[Initialiser le module HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) | La plupart des configurations nécessitent l'initialisation du dispositif HSM. Sans cela, seules certaines commandes `show` pourront être exécutées.
[Créer une partition](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition) | Une partition est un espace logique et indépendant associé au client qui demande ou crée des objets cryptographiques dans le moteur HSM.
[Installer le logiciel client HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software) | Dans cette sous-section, VPX sera installé avec le logiciel et les utilitaires requis pour interagir avec le module HSM. |
[Etablir une connexion NTL](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) | Un lien de confiance de réseau (NTL) est un canal de communication sécurisé entre le module de sécurité matérielle HSM (Hardware Security Module) et le client. |
[Créer des clés et générer la demande de signature de certificat (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) | Dans cette sous-section, nous allons créer une paire de clés qui sera utilisée pour générer une demande de signature de certificat (CSR), puis commander/demander un certificat par son intermédiaire. |
[Commander le certificat](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) | Commandez un certificat SSL pour votre {{site.data.keyword.vpx_full}}.
[Extraire et transférer le certificat](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) | Récupérez le certificat SSL commandé précédemment en vue de l'utiliser pour l'installation et la configuration décrites à l'étape suivante.
