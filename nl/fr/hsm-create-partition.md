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

# Création d'une partition
{: #create-a-partition}

Une partition est un espace logique et indépendant associé au client qui demande ou crée des objets cryptographiques dans le moteur HSM. Chaque partition possède ses propres données et stratégies isolées des autres partitions. Pour en savoir plus sur les partitions, consultez le document [Administration Guide (page 211) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}.

Pour créer une partition, procédez comme suit :

1.	Connectez-vous en tant que responsable de la sécurité/administrateur HSM à l'aide du mot de passe spécifié lors de l'[initialisation](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) :

	```
	[jpmongehsm2] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```

2.	Vérifiez que le statut de connexion HSM Admin est “Logged In” :

	```
	[jpmongehsm2] lunash:>hsm show

	Appliance Details:
	==================
	Software Version:                6.2.2-5

	HSM Details:
	============
	HSM Label:                          jpmonge
	Serial #:                           534071
	Firmware:                           6.10.9
	HSM Model:                          K6 Base
	Authentication Method:              Password
	HSM Admin login status:             Logged In
	HSM Admin login attempts left:      3 before HSM zeroization!
	RPV Initialized:                    No
	Audit Role Initialized:             No
	Remote Login Initialized:           No
	Manually Zeroized:                  No
	[OUTPUT OMITTED]
	```

	La sortie ci-dessus doit indiquer `Logged In` dans la zone HSM Admin login status. Sinon, la plupart des opérations et des commandes répertoriées dans les sections suivantes n'aboutiront pas, car elles nécessitent un accès administrateur.

3.	Dressez la liste de toutes les partitions existantes :

	```
	[jpmongehsm2] lunash:>partition list
	Storage (bytes)
	----------------------------
	Partition            Name                   Objects   	Total    Used    Free
	===================================
	534071016            partition1                   0  207559       0  207559 	534071020            partition2                   3  207559    3464  204095
	534071027            partition3                   0  207559       0  207559
	534071021            partition4                   2  207559    1652  205907
	534071030            partition5                  10  207559    9400  198159

	Command Result : 0 (Success)
	```

	La sortie ci-dessus indique qu'il existe cinq partitions.

4.	Créez une nouvelle partition :

	**Remarque :** Le mot de passe défini à cette étape sera utilisé ultérieurement pour associer et créer des objets dans le processus client Citrix VPX HSM. Nous vous recommandons de garder une trace de ce mot de passe de manière à pouvoir le retrouver si vous en avez besoin. Veillez également à utiliser le domaine de clonage défini lors du processus d'initialisation.

	```
	[jpmongehsm2] lunash:>partition create -partition partition6

	On completion, you will have this number of partitions: 6

	-label:  Not provided; using name for label.

	Please enter a password for the partition:
	> **********

	Please re-enter password to confirm:
	> **********

	Please enter a cloning domain to use when creating this partition:
	> ********

	Please re-enter cloning domain to confirm:
	> ********

	Type 'proceed' to create the initialized partition, or 'quit' to quit now.
		> proceed
	'partition create' successful.

	Command Result : 0 (Success)
	```

	La syntaxe étant la suivante :

	```
	partition create -partition <name-for-new-Partition>
	```

5.	Vérifiez que la nouvelle partition a été créée :

	```
	[jpmongehsm2] lunash:>partition list

	Storage (bytes)	                                             	----------------------------
	Partition            Name                   Objects   Total    Used    Free
	===========================================
	534071016            partition1                   0  207559       0  207559
	534071020            partition2                   3  207559    3464  204095
	534071027            partition3                   0  207559       0  207559
	534071021            partition4                   2  207559    1652  205907
	534071030            partition5                  10  207559    9400  198159
	534071053            partition6                   0  207559       0  207559

	Command Result : 0 (Success)
	```

	Le résultat de la commande `Partition List` indique maintenant 6 partitions.
