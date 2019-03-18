---



copyright:
  years: 2017
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configuration de la redirection vers un cache du trafic SSL (en option)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

Au lieu de configurer la redirection de cache du serveur virtuel avec un protocole HTTP ou HTTPS (comme indiqué à l'étape précédente), vous pouvez configurer la redirection vers SSL. 

Pour ce faire, procédez comme suit :

1. Accédez à **Traffic Management > Cache Redirection > Virtual Servers** et cliquez sur **Add**. Indiquez le nom de votre serveur virtuel à proxy direct, choisissez le protocole SSL et le type de cache **FORWARD**. Attribuez-lui une adresse IP de votre sous-réseau privé, avec le port requis. 

	<img src="images/fp14.png" alt="dessin" style="width: 300px;"/>

	Cliquez sur **OK**. 
	
2. Passez en revue la page de récapitulatif et cliquez sur **OK** pour continuer.
3. Spécifiez les paramètres Redirect, DNS Virtual Server et Destination Virtual Server. 
4. Cliquez sur **Certificate** sous **Advanced Settings** pour afficher la configuration par certificat SSL. 
5. Cliquez sur la zone vide **No Server Certificate**.
6. A partir de la liste déroulante Select Server Certificate, sélectionnez votre serveur SSL.
7. Entrez les informations de configuration du certificat comme requis.

	<img src="images/fp15.png" alt="dessin" style="width: 400px;"/>

	Cliquez sur **Install**.
	
8. Sélectionnez **Bind**.

	<img src="images/fp16.png" alt="dessin" style="width: 300px;"/>
