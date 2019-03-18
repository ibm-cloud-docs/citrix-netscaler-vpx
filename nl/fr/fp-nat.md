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

# Configuration de la conversion NAT source pour le trafic sortant
{: #configure-source-nat-for-outbound-traffic}

La conversion d'adresses réseau (NAT) est une méthode de remappage d'un espace d'adresse IP à un autre en modifiant les informations d'adresse réseau dans l'en-tête IP des paquets lorsqu'ils sont en cours d'acheminement sur un périphérique de routage de trafic.

Vous pouvez utiliser votre dispositif Citrix NetScaler VPX pour effectuer une conversion NAT sur le trafic sortant depuis vos machines client. Pour ce faire, procédez comme suit :

1. Accédez à System > Network > Routes, et sélectionnez l'onglet **RNAT**. Cliquez sur **Configure RNAT**.

2. Spécifiez le sous-réseau source (et masque) auquel vous souhaitez appliquer RNAT, puis cliquez sur **OK**.

Le trafic Internet provenant de n'importe quelle IP de ce sous-réseau utilisera désormais la conversion NAT pour le trafic sur l'adresse IP publique de Citrix NetScaler.    
