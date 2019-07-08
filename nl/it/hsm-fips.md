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

# Abilita FIPS 140-2 (facoltativo)
{: #enable-fips-140-2-optional-}

FIPS (Federal Information Processing Standards) è una serie di standard per la specifica dei requisiti di sicurezza quando si implementa l'hardware e il software crittografico. È stato creato nel 1994 ed è stato rilasciato un aggiornamento a questo standard nel 2001, noto come FIPS 140-2.

Gli algoritmi di sicurezza FIPS 140-2 possono essere abilitati se hai bisogno di garantire che l'HSM (Hardware Security Module) sia compatibile e conforme con le agenzie e i governi che utilizzano FIPS. Questa sezione fornisce le istruzioni su come farlo.

1. Prima di tutto, conferma che la modalità FIPS sia al momento disabilitata, utilizzando il comando `hsm show`.

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

	The output states `The HSM is NOT in FIPS 140-2 approved operation mode`, confirming the device is not running FIPS.

2. Controlla le tue politiche prima di abilitare la modalità FIPS con il comando `hsm showpolicies`.

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[OUTPUT OMITTED]

	The following policies are set due to current configuration of this HSM and cannot be altered directly by the user.

	Description                              Value
	===========                              =====

	PIN-based authentication                  True

	The following policies describe the current configuration of this HSM and may be changed by the HSM Administrator.

	Changing policies marked "destructive" will zeroize (erase completely) the entire HSM.

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

	This output shows that policy 12 (`Allow non-FIPS algorithms`) is set to `On`, meaning that algorithms non-compliant with FIPS are currently allowed for operations in the HSM.

3. Accedi come un HSM SO/amministratore utilizzando la password che hai specificato durante l'[inizializzazione](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-).

	```
	[jdoe1] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```
	{: screen}

4. Abilita la modalità FIPS 140-2.

	To enable FIPS mode, you must modify the policy reviewed in step two of this procedure, (`Allow non-FIPS algorithms`):

	This procedure will erase any existing partitions in the HSM. If you already created partitions and objects, make sure to review the partition contents and configurations in order to recreate them when the new partitions are created.
	{: note}

	Use the `hsm changepolicy` command to disable policy 12 and only allow the usage of FIPS algorithms:

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

5. Conferma che la modalità FIPS sia ora abilitata utilizzando ancora una volta il comando `hsm show`.

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

	The command `hsm showpolicies` should now show that the device is using the FIPS 140-2 mode on policy (code) 12, and reflect the enforcement of FIPS 140-2 algorithms:

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[OUTPUT OMITTED]

	The following policies are set due to current 	configuration of this HSM and cannot be altered directly by the user.

	Description                              Value
	===========                              =====
	PIN-based authentication                 True

	The following policies describe the current configuration of this HSM and may be changed by the HSM Administrator. Changing policies marked "destructive" will zeroize (erase completely) the entire HSM.

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
