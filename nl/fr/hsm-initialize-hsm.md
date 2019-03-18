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

# Initialisation du module de sécurité matérielle IBM HSM (Hardware Security Module)
{: #initialize-ibm-hardware-security-module-hsm-}

La plupart des configurations nécessitent l'initialisation du dispositif HSM. Sans cela, seules certaines commandes `show` pourront être exécutées.

Pour initialiser le dispositif, procédez comme suit :

1.	Connectez-vous, via SSH, au module IBM HSM en utilisant les informations d'identification fournies sur le portail de contrôle sous **Devices > Device List > Expand HSM name**.

	Il est également possible d'utiliser l'authentification par clé publique. Si besoin, consultez le document [Appliance Administration Guide (page 38) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}.

	**Remarque :** L'accès via SSH est généralement activé et autorisé par défaut. Si vous rencontrez des problèmes de connexion avec SSH, vérifiez les paramètres de routage et de sécurité de votre infrastructure.

2. Exécutez la commande `hsm init` :

	```
	[jpmongehsm2] lunash:>hsm init -l jpmonge

	Please enter a password for the HSM Administrator:
	> ********

	Please re-enter password to confirm:
	> ********

	Please enter a cloning domain to use for initializing this HSM:
	> ********

	Please re-enter cloning domain to confirm:
	> ********

	CAUTION:  Are you sure you wish to initialize this HSM?

	Type 'proceed' to initialize the HSM, or 'quit'
		to quit now.
		> proceed
		'hsm init' successful.

	Command Result : 0 (Success)
  	```

	Où la syntaxe utilisée est la suivante : `hsm init -l <hsmlabel>`

Le paramètre ou libellé `-l` sert à attribuer un identificateur à HSM. Il peut s'agir d'un texte ou d'une description suffisamment clairs pour le secteur, l'administrateur ou le rôle qu'il remplit. Le mot de passe administrateur est le mot de passe du responsable de la sécurité HSM et correspond essentiellement à un profil requis pour créer et configurer des objets cryptographiques, ainsi que pour apporter des modifications à l'environnement de HSM.

Enfin, le domaine de clonage représente un identificateur partagé qui permet de former des objets parmi un groupe de modules HSM. Ce domaine est généralement utilisé à des fins de sauvegarde et/ou de haute disponibilité.

Reportez-vous au document [LunaSH Command Reference Guide (en anglais)![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window} pour en savoir plus sur les commandes prises en charge par l'interface CLI de HSM.
