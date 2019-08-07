---

copyright:
  years: 2019
lastupdated: "2019-04-08"

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

# Activation des fonctionnalités requises dans {{site.data.keyword.vpx_full}} 
{: #enable-required-features-in-vpx}

Vous pouvez activer les fonctionnalités requises dans VPX pour créer le VPN IPSec : 

1.	Accédez à l’interface utilisateur graphique VPX. 
2.	Accédez à **System > Settings > Configure Modes** et activez **Layer 3 Mode (IP Forwarding)**.
3.	Accédez à **System > Settings > Configure Advanced Features** et activez **Cloud Bridge**.

Pour activer ces fonctions dans l'interface CLI, exécutez les commandes suivantes :

```
> enable ns feature CloudBridge
> enable ns mode L3

```

Pour des instructions supplémentaires sur la connexion à NetScaler à l'aide de l'interface graphique ou de SSH, consultez l'[article suivant](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler). 
