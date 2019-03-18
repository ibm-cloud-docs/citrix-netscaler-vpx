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

# Configuration du serveur virtuel DNS
{: #configure-the-dns-virtual-server}

Pour configurer un serveur virtuel DNS :

1. Accédez à Traffic Management > Load Balancing > Servers. 
2. Cliquez sur Add pour ajouter les deux résolveurs DNS IBM© Softlayer, 10.0.80.11 et 10.0.80.12. 

	<img src="images/fp5.png" alt="dessin" style="width: 200px;"/> <img src="images/fp5b.png" alt="dessin" style="width: 200px;"/>

3. Ensuite, créez et définissez votre groupe de services DNS en accédant à Traffic Management > Load Balancing > Service Groups, et en choisissant Add. 

	<img src="images/fp6.png" alt="dessin" style="width: 400px;"/> 

4. Sélectionnez le protocole DNS et cliquez sur OK.

	<img src="images/fp7.png" alt="dessin" style="width: 300px;"/> 
	
5. Sur l'écran suivant, ajoutez les nouveaux résolveurs DNS comme serveurs membres du groupe de services DNS en cliquant d'abord sur la zone vide située sous **Service Group Members**. 

6. Dans le panneau Create Service Group Member, spécifiez le port DNS 53, puis cliquez sur Create. 

	<img src="images/fp8.png" alt="dessin" style="width: 200px;"/> 
	
7. Cliquez sur Close, puis sur Done. 

	Si les deux résolveurs DNS IBM Softlayer sont accessibles à partir de votre dispositif Citrix NetScaler VPX, le groupe de services s'affichera en vert. 

8. Accédez ensuite à Traffic Management > Load Balancing > Virtual Servers et cliquez sur Add pour définir votre serveur virtuel DNS.
9. Sous Basic Settings, attribuez un nom à votre serveur virtuel, choisissez le protocole DNS et le port 53, puis affectez une adresse IP à partir de votre sous-réseau privé. 

	<img src="images/fp9.png" alt="dessin" style="width: 300px;"/> 
	
10. Sur la page suivante, cliquez sur la zone vide intitulée **No Load Balancing virtual Server ServiceGroup Binding**.
11. Sélectionnez votre groupe de services DNS préalablement défini dans la liste déroulante et cliquez sur Bind.  

	<img src="images/fp10.png" alt="dessin" style="width: 300px;"/> 
	
12. Cliquez sur Continue, puis sur Done. 

L'état de votre serveur virtuel DNS doit maintenant apparaître en vert. 

<img src="images/fp11.png" alt="dessin" style="width: 500px;"/> 
