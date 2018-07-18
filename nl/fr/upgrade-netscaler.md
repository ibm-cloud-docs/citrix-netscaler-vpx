---
copyright:
  years: 1994, 2018

lastupdated: "2018-06-28"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Mise à niveau de votre Citrix NetScaler VPX

**REMARQUE :** Vous devez être connecté au VPN avant de tenter cette procédure.

1. Connectez-vous à l'IP de gestion de NetScaler.
2. Cliquez sur **System Upgrade**.
4. Sélectionnez **Local** dans la liste déroulante **Choose File**. 
4. Téléchargez le fichier de mise à niveau correct à partir de l'emplacement suivant :

	[Versions disponibles de NetScaler ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}
	
	**REMARQUE :** Vous devez être connecté au VPN de l'infrastructure IBM Cloud pour pouvoir accéder à ce lien.

5. Sur l'écran Upload Software, allez à l'emplacement du fichier de mise à niveau et cliquez sur **Upgrade**. Le microprogramme se télécharge.
6. Sur la fenêtre System Upgrade qui s'affiche, vous serez invité à réamorcer. Cliquez sur **Close**.
7. Revenez à **System** et cliquez sur **Reboot**.
8. Après la mise à niveau, fermez toutes les instances de navigateur et effacez le cache de votre ordinateur avant d'accéder au dispositif.

**REMARQUE :** L'interface utilisateur peut varier en fonction de la version de votre NetScaler VPX.



