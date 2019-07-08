---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, certificate, order

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

# Commande d'un certificat SSL
{: #order-an-ssl-certificate}

Secure Sockets Layer (SSL) est une technologie qui chiffre le trafic entre l'application client et l'application serveur par le biais d'un système de clés publique/privée utilisant un certificat SSL.

Les certificats SSL contiennent la clé publique du serveur, les dates de validité du certificat, un nom d'hôte valide et la signature de l'autorité de certification qui a émis le certificat.

IBM© Cloud offre la possibilité d'acquérir/acheter des certificats sans avoir à passer par un fournisseur/site tiers.

IBM Cloud propose des certificats SSL annuels et biannuels qui offrent divers avantages, notamment :

* Authentification complète pour la vérification d'identité de l'entreprise et de l'appartenance du domaine
* Chiffrement sur 40 à 256 bits pour toutes les transactions en ligne
* Recherche quotidienne de logiciels malveillants sur le site web pour garantir sa protection ainsi que celle de vos clients

Si vous exploitez plusieurs domaines, vous pouvez acheter un certificat SSL pour chacun d'eux.

Pour plus d'informations sur les certificats SSL, consultez les articles IBM Cloud suivants :

* [A propos des certificats SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [Introduction à la technologie SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [Planification pour SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)


Pour commander un certificat SSL à utiliser avec votre Citrix NetScaler VPX, procédez comme suit :

1.	A partir de l'interface CLI du shell VPX, affichez le texte CSR en ouvrant le fichier CSR précédemment créé à l'étape [Création de clés et génération de la demande de signature de certificat (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-):

	```
	root@IBMADC690867-s6dr# cat certreqnss6dr.csr
	-----BEGIN NEW CERTIFICATE REQUEST-----
	MIIC5jCCAc4CAQAwgaAxCzAJBgNVBAYTMRcwFQYDVQQIEw5Ob3J0aCBDYXJv
	bGluYTEPMA0GA1UEBxMGRHVyaGFtMQwwCgYDVQQKEwNJQk0xDDAKBgNVBAsTA0hT
	TTEoMCYGA1UEAxMfaHNW50Ny5wcm9qZWN0Z29sZGZpbmNoLm5ldDEhMB8G
	CSqGSIb3DQEJARYSanBtb25nZUBjci5pYm0uY29tMIIBIjANBgkqhkiG9w0BAQEF
	/pXQN+a55HhWmnyj5gThAprOoN8DeiVN+1HI+PA+g1
	r4+8dKA1xz+jPhWDQgQYb3Wnh8VK8Ouids6uFnsoc3KDymbzoWZYctp8PA6uBzJ/
	25RGiZquRu9MYJIWkQ46WQ14PoJ8BiYuJa/N6L47+Jr2vaCntmXBU4rFrjctHqq8
	Hct9q5OVYXbYLQB+MM3gYyyFBQpZ1sHZD4D6K3AISRGsOE9rrovGjUfO8mLKE6a
	AQEFBQADggEBAMe+kmdPNtt8LOpaAy+u5i9GpgHfH5zW2sX4Lj7srkqwmyxavqjE
	XvM9PPudXV9OCUWewtlm/Eqo1pYIRudFBrjg5UJyKpM4sWWdKIrTk8RZusdOUvKU
	0vBRJRJ3Yy/1olXFO05FFSotAyB9P5v9siMwdWUhM9pSiGwoNXCB74m2sxgUh10J
	H0IvDl3SL4ptosV10KJtbOiO/YV9XXNaW8/X/2uM9Y3stcnSvzJGrFlPmbhK7Vsd
	uL6/wSnV1E70CDT+KPPapzVJr/S8nP5xHVVl/5/JUGZa8rx01g9EBmX36H3T
	kHD85XOkSI4y04Y3t6pMVbIAz0vipOmHYlM=
	-----END NEW CERTIFICATE REQUEST-----
	```

2.	Copiez le contenu du fichier à partir de `---BEGIN NEW CERTIFICATE REQUEST---` jusqu'à `---END NEW CERTIFICATE REQUEST---`.

3.	Suivez [ces instructions](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates) pour effectuer la commande, en collant le texte de votre CSR dans la zone appropriée. Dans l'exemple ci-dessous, `RapidSSL 1 Year` a été choisi.

	<img src="images/5-Order-Certificate_1.png" alt="dessin" style="width: 550px;"/>

	Comme indiqué, le système traite et interprète le texte CSR, puis l'affiche à la page suivante.

	Assurez-vous de sélectionner un compte de messagerie et un domaine/sous-domaine valides, car il s'agit de la méthode désignée pour valider la propriété du domaine.

	Confirmez les détails de la commande et cliquez sur **Valider la commande**.

4. Vous recevrez une confirmation de commande avec les détails de la demande de certificat sur le compte que vous avez indiqué.

	Cliquez sur le lien inclus dans l'e-mail pour approuver la demande de validation du domaine. A ce stade, la demande SSL doit être prête à être exécutée.
