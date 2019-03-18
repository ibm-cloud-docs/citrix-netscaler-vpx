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

# Configuration de la redirection vers un cache du trafic HTTP(S)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

Pour configurer la redirection du trafic HTTP ou HTTPS vers un cache, procédez comme suit :

1. Accédez à **Traffic Management > Cache Redirection > Virtual Servers** et cliquez sur **Add**.
2. Indiquez le nom de votre serveur virtuel à proxy direct. Sélectionnez le protocole **HTTP** et le type de cache **Forward** dans leurs listes déroulantes respectives. Affectez ensuite une adresse IP au serveur virtuel à partir de votre sous-réseau virtuel.

	<img src="images/fp12.png" alt="dessin" style="width: 300px;"/>

	Cliquez sur **OK** pour continuer.

3. Passez en revue la page de récapitulatif et cliquez sur **OK**.  
4. Cliquez sur **Traffic Settings** pour afficher des paramètres de configuration supplémentaires.
5. Choisissez l'une des trois options de redirection ci-dessous, selon vos besoins :
	* **Cache** - Dirige toutes les demandes sortantes vers votre pool de serveurs de cache local.
	* **Policy** - Vérifie la stratégie de redirection de cache pour déterminer si la demande doit être transmise au pool de serveurs de cache ou aux serveurs de destination (origine).
	* **Origin** – Dirige toutes les demandes sortantes vers les serveurs de destination respectifs (origine).

6. Dans la liste déroulante **DNS Virtual Server Name**, sélectionnez le serveur virtuel DNS précédemment configuré et définissez l'option **Redirect** sur **Origin**.

	<img src="images/fp13.png" alt="dessin" style="width: 300px;"/>

	**Remarque :** Le paramètre **Destination Virtual Server** est utilisé lorsque le trafic sortant doit être dirigé vers le pool de serveurs de cache local. Laissez-le vide si vous souhaitez diriger l'ensemble du trafic sortant vers les serveurs d'origine.

7. Cliquez sur **OK**, puis sur **Done**.
