---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: partition, create, security, hsm

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

# Creazione di una partizione
{: #create-a-partition}

Una partizione è uno spazio logico e indipendente associato o collegato al client che sta richiedendo o creando oggetti crittografici nel motore HSM. Ciascuna partizione dispone di propri dati e politiche isolati dalle altre partizioni. Per ulteriori informazioni sulle partizioni, consulta la [Administration Guide (pagina 211) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}.

Per creare una partizione, esegui la seguente procedura:

1.	Accedi come responsabile della sicurezza/amministratore (Security Officer/Administrator) HSM utilizzando la password specificata durante l'[inizializzazione](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-):

	```
	[jpmongehsm2] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```

2.	Conferma che il valore di HSM Admin Login Status sia “Logged In”:

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

	L'output sopra riportato mostra `Logged In` nel campo HSM Admin login status. In caso contrario, molti dei comandi e delle operazioni elencati nelle seguenti sezioni avranno esito negativo in quanto richiedono l'accesso amministratore (Administrator).

3.	Elenca le partizioni esistenti:

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

	Questo output mostra cinque partizioni esistenti.

4.	Crea una nuova partizione:

	 La password definita in questo passo verrà utilizzata in un secondo momento per associare e creare oggetti nel processo client HSM Citrix VPX. Tieni traccia di questa password per riferimento futuro. Inoltre, assicurati di utilizzare il dominio di clonazione durante il processo di inizializzazione.
   {: note}

	```
	[jpmongehsm2] lunash:>partition create -partition partition6

	Al completamento, avrai questo numero di partizioni: 6

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

	Dove la sintassi è:

	```
	partition create -partition <name-for-new-Partition>
	```

5.	Conferma che la nuova partizione è stata creata:

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

	L'output del comando `Partition List` mostra ora sei partizioni.
