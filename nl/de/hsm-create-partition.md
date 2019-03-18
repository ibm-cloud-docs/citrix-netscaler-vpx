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

# Partition erstellen
{: #create-a-partition}

Eine Partition ist ein logischer und unabhängiger Speicherbereich, der dem Client zugeordnet ist, der Verschlüsselungsobjekte in der HSM-Engine anfordert oder erstellt. Jede Partition verfügt über eigene Daten und Richtlinien, die von anderen Partitionen isoliert sind. Weitere Informationen zu Partitionen finden Sie im [Administratorhandbuch (Seite 211) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}.

Gehen Sie wie folgt vor, um eine Partition zu erstellen:

1.	Melden Sie sich mit dem Kennwort, das während der [Initialisierung](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) angegeben wurde, als HSM-Sicherheitsbeauftragter/Administrator an:

	```
	[jpmongehsm2] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```

2.	Vergewissern Sie sich, dass der 'HSM Admin Login Status' 'Logged In' lautet:

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

	In der vorangegangenen Ausgabe muss für 'HSM Admin login status' (Anmeldestatus des HSM-Administrators) `Logged In` (Angemeldet) erscheinen. Andernfalls schlagen die meisten der in den folgenden Abschnitten aufgeführten Operationen und Befehle fehl, da hierfür Administratorzugriff erforderlich ist.

3.	Listen Sie alle vorhandenen Partitionen auf:

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

	In dieser Ausgabe werden fünf vorhandene Partitionen angezeigt.

4.	Erstellen Sie eine neue Partition:

	**HINWEIS:** Das in diesem Schritt definierte Kennwort wird später für die Zuordnung und Erstellung von Objekten im Citrix VPX HSM-Clientprozess verwendet. Behalten Sie dieses Kennwort für zukünftige Referenzen bei. Stellen Sie außerdem sicher, dass die während des Initialisierungsprozesses definierte Klondomäne verwendet wird.

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

	Die Syntax lautet hierbei wie folgt:

	```
	partition create -partition <Name-der-neuen-Partition>
	```

5.	Überprüfen Sie, ob die neue Partition erstellt wurde:

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

	In der Ausgabe des Befehls `Partition List` werden jetzt sechs Partitionen angezeigt.
