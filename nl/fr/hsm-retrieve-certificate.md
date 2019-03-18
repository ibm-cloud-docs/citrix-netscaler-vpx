---

copyright:
  years: 2018
lastupdated: "2018-11-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Extraction et transfert du certificat
{: #retrieve-and-transfer-the-certificate}

Récupérez le certificat SSL que vous avez commandé précédemment afin d'être prêt pour son installation et sa configuration décrites dans la rubrique suivante, [Configuration et optimisation du déchargement SSL avec Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx).

1. Peu de temps après la validation de la propriété du domaine, vous devriez recevoir un courrier électronique confirmant l'exécution du certificat et validant le certificat lui-même.

	Copiez le texte à partir de `---BEGIN CERTIFICATE---` jusqu'à `---END CERTIFICATE---` et enregistrez le contenu dans un nouveau fichier certificat avec l'extension `.cer`.

2. Copiez le fichier certificat dans le répertoire `/nsconfig/ssl` de Citrix NetScaler VPX.

<img src="images/11-transfer-certificate.png" alt="dessin" style="width: 600px;"/>

Citrix NetScaler VPX est maintenant prêt à intégrer le certificat dans un déploiement d'équilibrage de charge via SSL.
