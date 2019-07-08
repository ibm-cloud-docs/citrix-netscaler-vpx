---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: ha, high availability, setup, configure, configuration

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Configuration de Citrix Netscaler VPX pour la haute disponibilité
{: #setting-up-citrix-netscaler-vpx-for-high-availability-ha-}

Les équilibreurs de charge servent à répartir le trafic sur plusieurs serveurs d'application afin d'améliorer la performance et la stabilité d'une application échelonnable. Cependant, lorsqu'il est seul à assumer cette fonction, l'équilibreur de charge constitue un point unique de défaillance. Ce risque peut être évité par la configuration d'une paire de serveurs Netscaler VPX haute disponibilité. La configuration d'une paire haute disponibilité requiert deux serveurs Netscaler VPX. Le serveur secondaire intervient pour poursuivre l'équilibrage de charge en cas de panne du serveur primaire.

La SNIP (SubNet IP) est l'IP que les serveurs recevant une part de la charge équilibrée voient comme IP source des demandes (connexions) adressées à la VIP (IP virtuelle) du Netscaler VPX. Normalement, dans une configuration en paire haute disponibilité, la SNIP ne change pas, excepté en cas d'événement de reprise par basculement (failover). Dans ces conditions, lorsque les deux équilibreurs sont dans le même sous-réseau, la SNIP du NetScaler VPX secondaire peut changer pour devenir la SNIP qui était utilisée à l'origine par le NetScaler VPX primaire. Cela n'entraîne aucune confusion pour les serveurs auxquels la demande est adressée.

Pour une configuration haute disponibilité, les deux NetScalers doivent être dans le même VLAN et sur le même sous-réseau.

Avant de commencer la configuration haute disponibilité, veillez à entreprendre les actions prérequises suivantes :

1. S'il est prévu que la paire ait une configuration active-active, tous les sous-réseaux de VIP ajoutés aux instances doivent être du type "Routed to VLAN".
2. S'il est prévu que la paire ait une configuration active-passive, tous les sous-réseaux de VIP ajoutés aux instances doivent être soit du type "Routed to VLAN", soit du type "Secondary routed to IP" et routés vers l'adresse IP publique du noeud primaire.

Après avoir passé commande des deux serveurs NetScaler VPX dans le VLAN nécessaire et des VIP et sous-réseaux SNIP répondant aux prérequis de votre configuration en paire haute disponibilité, vous pouvez enchaîner avec les étapes suivantes :

1. Ouvrez deux fenêtres de navigateur et, dans chacune d'elles, connectez-vous à l'interface avancée de l'un des deux NetScalers. Dans l'interface de gestion du NetScaler VPX secondaire, allez dans **System > User Administration > Users** et définissez le même mot de passe root que celui du NetScaler VPX primaire. Répercutez ensuite ce changement sur le portail {{site.data.keyword.BluSoftlayer_notm}}, dans la page des détails de l'appareil, afin de rendre le mot de passe identique à celui que vous venez de définir pour le NetScaler secondaire.

2. Dans le NetScaler VPX que vous choisissez de désigner comme secondaire, cliquez sur **System > High Availability**, puis faites un clic droit sur la première ligne et cliquez sur **Edit**. Sélectionnez **Stay Secondary** dans la liste déroulante High Availability Status config et cliquez sur **OK**.

3. Sélectionnez **Add**. Entrez l'adresse IP système de l'autre NetScaler VPX (située sous l'onglet High Availability sur le VPX primaire), ainsi que les détails de connexion root en bas de la fenêtre. Laissez la case **Turn on INC** (Independent Network Configuration) non cochée. Cliquez sur **OK**.

	Si un message d'erreur vous signale que les IP ne sont pas dans le même sous-réseau, c'est peut-être parce que les deux serveurs VPX ne sont pas dans le même VLAN. Autrement, vous devriez maintenant pouvoir ouvrir le serveur primaire et sélectionner le bouton **Refresh** pour voir les deux serveurs fonctionner en paire haute disponibilité.

	La nouvelle IP de gestion du NetScaler secondaire est une adresse IP en dessous de la précédente. Si vous ne pouvez pas accéder au VPX secondaire, supprimez la haute disponibilité à partir de la ligne de commande en utilisant la commande :

	`sh ha node`

	Supprimez ensuite ce qui devrait être le noeud haute disponibilité (ha) :

	`rm ha node 1`

4. Sur le VPX primaire, vous devez voir que le VPX distant est en cours de synchronisation. Allez dans l'interface de gestion du VPX secondaire et vérifiez sa configuration **Network > IPs**. La VIP du VPX primaire et les autres IP doivent être indiquée comme étant passives.

6. Retournez à **System > High Availability** sur le serveur secondaire et cliquez sur **Edit**. Sélectionnez **ENABLED** dans la liste déroulante et cliquez sur **OK**.

7. Testez un basculement en le forçant (action Force Failover). Actualisez l'écran et observez les adresses IP devenir actives sur le VPX secondaire. Forcez un autre basculement et observez-les devenir passives. Vérifiez que les IP sont joignables en leur envoyant un ping.

8. Le VPX primaire doit à présent est libellé comme tel et le VPX secondaire doit se signaler à l'état synchronisé.
