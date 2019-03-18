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

# Ajout et configuration du serveur virtuel SSL
{: #add-and-configure-the-ssl-virtual-server}

Pour ajouter et configurer un serveur virtuel SSL, procédez comme suit :

1. Accédez à **System > Settings > Configure Basic Features**. Sélectionnez l'option de **déchargement SSL** et cliquez sur **OK**.
2. Dans l'interface graphique utilisateur de NetScaler, accédez à **Traffic Management > Load Balancing > Services > Add**, spécifiez le nom, l'adresse IP, puis définissez le protocole **HTTP**. Cliquez sur **OK** pour finir.
3. Vérifiez que le service est opérationnel :

	<img src="images/15-confirm-service.png" alt="dessin" style="width: 700px;"/>

4. Répétez l'étape 2 pour tous les serveurs supplémentaires.
5. Accédez à **Traffic Management > Load Balancing > Virtual Servers >** et cliquez sur **Add**. Entrez le nom, sélectionnez le protocole **SSL**, puis entrez l'adresse IP publique. Cliquez sur **OK** pour finir.
6. Sélectionnez ensuite **No Load Balancing Virtual Server Service Binding** et cliquez sur **Select**. Sélectionnez le ou les services que vous avez créé(s) aux étapes précédentes, cliquez sur Select, puis sur **Bind/Continue**.

	<img src="images/18-bind-service.png" alt="dessin" style="width: 700px;"/>

7. Pour finir, cliquez sur **No Server Certificate**, puis sur **Select Server Certificate** et sélectionnez le certificat que vous avez préalablement installé. Cliquez sur **Select**, puis sur **Bind/Continue** et **DONE** pour terminer.
