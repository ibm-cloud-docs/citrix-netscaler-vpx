---

copyright:
  years: 2018
lastupdated: "2019-03-27"

keywords: security, hsm, fips

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:tip: .tip}
{:important: .important}

# Activation de FIPS 140-2 (facultatif) 
{: #enable-fips-140-2-optional-}

FIPS (Federal Information Processing Standards) est un ensemble de normes permettant de spécifier les exigences de sécurité lors de la mise en oeuvre de matériel et de logiciels cryptographiques. Il a été créé en 1994 et une mise à jour de cette norme a été publiée en 2001, sous le nom de FIPS 140-2. 

Les algorithmes de sécurité FIPS 140-2 peuvent être activés si vous devez vous assurer que le module de sécurité matérielle (Hardware Security Module - HSM) est compatible et conforme aux agences et aux gouvernements opérant sous FIPS. Cette section fournit des instructions pour ce faire. 

1. Tout d’abord, vérifiez que le mode FIPS est actuellement désactivé à l’aide de la commande `hsm show`.

	```
	[jdoe1] lunash:>hsm show

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
	HSM Admin login status:             Not Logged In
	HSM Admin login attempts left:      3 before HSM zeroization!
	RPV Initialized:                    No
	Audit Role Initialized:             No
	Remote Login Initialized:           No
	Manually Zeroized:                  No

	[OUTPUT OMITTED]

	FIPS 140-2 Operation:
	=====================
	The HSM is NOT in FIPS 140-2 approved operation mode.

	HSM Storage Information:
	========================
	Maximum HSM Storage Space (Bytes):   2097152
	Space In Use (Bytes):                1468005
	Free Space Left (Bytes):             629147
	Command Result : 0 (Success)
	```
	{: screen}

	La sortie indique `The HSM is NOT in FIPS 140-2 approved operation mode`, confirmant que le périphérique n'exécute pas FIPS.

2. Passez en revue vos règles avant d'activer le mode FIPS avec la commande `hsm showpolicies`.

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[OUTPUT OMITTED]

	Les règles suivantes sont définies en raison de la configuration actuelle de ce HSM et ne peuvent pas être modifiées directement par l'utilisateur.

	Description                              Value
	===========                              =====

	PIN-based authentication                  True

	Les règles suivantes décrivent la configuration actuelle de ce HSM et peuvent être modifiées par l'administrateur HSM.

	La modification des règles marquées "destructive" remet à zéro (efface complètement) tout le HSM.

	Description                             Value      Code      Destructive
	===========                             =====      ====      ===========
	Allow masking                            On         6            Yes
	Allow cloning                            On         7            Yes
	Allow non-FIPS algorithms                On         12           Yes
	SO can reset partition PIN               On         15           Yes
	Allow network replication                On         16           No
	Allow Remote Authentication              On         20           Yes
	Force user PIN change after set/reset    Off        21           No
	Allow offboard storage                   On         22           Yes
	Allow Acceleration                       On         29           Yes

	Command Result : 0 (Success)
	```
	{: screen}

	La sortie indique que la règle 12 (`Allow non-FIPS algorithms`) est définie sur `On`, ce qui signifie que les algorithmes non conformes à FIPS sont actuellement autorisés pour les opérations dans le HSM. 

3. Connectez-vous en tant que Responsable sécurité/Administrateur HSM à l'aide du mot de passe que vous avez spécifié lors de l'[initialisation](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-).

	```
	[jdoe1] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```
	{: screen}

4. Activez le mode FIPS 140-2. 

	Pour activer le mode FIPS, vous devez modifier la règle examinée à l'étape deux de cette procédure (`Allow non-FIPS algorithms`) :

	Cette procédure efface toutes les partitions existantes du HSM. Si vous avez déjà créé des partitions et des objets, veillez à examiner le contenu et les configurations de la partition afin de les recréer lors de la création des nouvelles partitions.
	{: note}

	Utilisez la commande `hsm changepolicy` pour désactiver la règle 12 et n'autoriser que l'utilisation des algorithmes FIPS : 

	```
	[jdoe1] lunash:>hsm changepolicy -policy 12 -value 0

	CAUTION: Are you sure you wish to change the destructive policy named:

	Allow non-FIPS algorithms

	Changing this policy will result in erasing all partitions on the HSM! (HSM Admin, Domain, and M of N (where applicable) will not be modified.

	Type 'proceed' to zeroize your HSM and change the policy, or 'quit' to quit now.

	> proceed

	'hsm changePolicy' successful.

	Policy Allow non-FIPS algorithms is now set to value: 0

	Command Result : 0 (Success)
	```
	{: screen}

5. Confirmez que le mode FIPS est maintenant activé en utilisant à nouveau la commande `hsm show`.

	```
	[jdoe1] lunash:>hsm show

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
	HSM Admin login status:             Not Logged In
	HSM Admin login attempts left:      3 before HSM zeroization!
	RPV Initialized:                    No
	Audit Role Initialized:             No
	Remote Login Initialized:           No
	Manually Zeroized:                  No

	Partitions created on HSM:
	==============================
	Partition:            534071009, Name: partition1
	Number of partitions allowed:        10
	Number of partitions created:        1

	FIPS 140-2 Operation:
	=====================
	The HSM is in FIPS 140-2 approved operation mode.

	HSM Storage Information:
	========================
	Maximum HSM Storage Space (Bytes):   2097152
	Space In Use (Bytes):                209715
	Free Space Left (Bytes):             1887437

	Command Result : 0 (Success)
	```
	{: screen}

	La commande `hsm showpolicies` doit maintenant indiquer que le périphérique utilise le mode FIPS 140-2 sur la règle (code) 12 et refléter l'application des algorithmes FIPS 140-2 :

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[OUTPUT OMITTED]

	Les règles suivantes sont définies en raison de la configuration actuelle de ce HSM et ne peuvent pas être modifiées directement par l'utilisateur. 

	Description                              Value
	===========                              =====
	PIN-based authentication                 True

	Les règles suivantes décrivent la configuration actuelle de ce HSM et peuvent être modifiées par l'administrateur HSM. La modification des règles marquées "destructive" remet à zéro (efface complètement) tout le HSM.

	Description                             Value        Code      Destructive
	===========                             =====        ====      ===========

	Allow masking                            On           6         Yes
	Allow cloning                            On           7         Yes
	Allow non-FIPS algorithms                Off          12        Yes
	SO can reset partition PIN               On           15        Yes
	Allow network replication                On           16        No
	Allow Remote Authentication              On           20        Yes
	Force user PIN change after set/reset    Off          21        No
	Allow offboard storage                   On           22        Yes
	Allow Acceleration                       On           29        Yes

	Command Result : 0 (Success)
	```
	{: screen}
