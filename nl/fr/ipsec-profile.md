---

copyright:
  years: 2019
lastupdated: "2019-04-28"

keywords: ipsec, vpn, vpx, tunnel

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

# Création d'un VPX de profil IPSec
{: #creating-ipsec-profile}

Le profil IPSec comprend des paramètres de sécurité pour l'établissement de connexions. Pour créer un profil, procédez comme suit : 

1.	Accédez à **Système > CloudBridge Connector > Profil IPSec** et cliquez sur **Ajouter**.
2.	Entrez les paramètres suivants : 
  *	**Nom**
  *	**Algorithme de chiffrement**
  *	**Algorithme de hachage**
  *	**Durée de vie**
3.	Sélectionnez la **Version du protocole IKE** appropriée.
4.	Cochez l'option **Confidentialité persistante parfaite (PFS)** si vous le souhaitez.
5.	Cochez l'option **La clé pré-partagée existe** et entrez la clé PSK dans la zone **Valeur**.
6.	Cliquez sur **Créer**.

    <img src="images/ipsecCreateProfile.png" alt="dessin" style="width: 200px;"/>

Pour créer un profil IPSec dans la CLI, utilisez la syntaxe suivante : 
  
  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra
  
  ```
