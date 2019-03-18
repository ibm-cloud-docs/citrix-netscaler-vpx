---
copyright:
  years: 1994, 2018
  
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Récentes mises à jour pour Citrix NetScaler VPX
{: #recent-updates-for-citrix-netscaler-vpx}

## Version 12.1

### Serveurs virtuels avec plusieurs adresses IP
Vous pouvez désormais créer un seul serveur virtuel à équilibrage de charge avec plusieurs adresses IPv4 et IPv6 consécutives ou non consécutives. Chaque adresse VIP liée à un serveur virtuel est traitée comme un serveur virtuel individuel.

Pour en savoir plus sur cette fonctionnalité, lisez l'article Citrix [Multiple IP virtual servers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window} (en anglais).

### SSL
Les mises à jour suivantes ont été appliquées pour les connexions SSL :
 
* Suppression du chiffrement faible du groupe de chiffrement DEFAULT_BACKEND. 
* Prise en charge du chiffrement ECDHE sur le module externe HSM front end de Thales nShield®
* Prise en charge du chiffrement ECDHE sur le module externe HSM front end du réseau SafeNet
* Suppression de SSLv2 : Le dispositif NetScaler VPX ne prend plus en charge SSLv2 à compter de la version 12.1.

De plus amples informations sur les mises à jour SSL 12.1 sont disponibles dans le document [Citrix 12.1 Release Notes ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window} (en anglais).

### Prise en charge des groupes de services pour GSLB
GLSB est maintenant compatible avec des groupes de services basés sur une adresse IP, des groupes de services basés sur un nom de domaine ou des groupes de services Autoscale basés sur un nom de domaine. De plus, vous pouvez gérer un groupe de services aussi facilement qu'un seul service, lier un groupe de services à un serveur virtuel, ou ajouter des services au groupe.

Pour plus d'informations sur les groupes de services GSLB, lisez l'article Citrix [Configuring a GSLB service group![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window} (en anglais).
