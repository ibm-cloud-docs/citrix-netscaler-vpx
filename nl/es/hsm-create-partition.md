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

# Crear una partición
{: #create-a-partition}

Una partición es un espacio lógico e independiente que está asociado o conectado al cliente que solicita o crea objetos criptográficos en el motor HSM. Cada partición tiene sus propios datos y políticas aislados de otras particiones. Para obtener más información sobre las particiones, consulte [Guía de administración (página 211) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}.

Para crear una partición, realice el procedimiento siguiente:

1.	Inicie sesión como Administrador/responsable de seguridad de HSM utilizando la contraseña especificada durante la [inicialización](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-):

	```
	[jpmongehsm2] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```

2.	Confirme que el estado del inicio de sesión del administrador de HSM es "Sesión iniciada":

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

	La salida anterior debe mostrar `Sesión iniciada` en el estado de inicio de sesión del administrador de HSM. De lo contrario, la mayoría de las operaciones y mandatos que se listan en las secciones siguientes fallarán puesto que requieren acceso de administrador.

3.	Liste las particiones existentes:

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

	Esta salida muestra cinco particiones existentes.

4.	Cree una nueva partición:

	 La contraseña definida en este paso se utilizará más adelante para asociar y crear objetos en el proceso de cliente HSM Citrix VPX. Realice un seguimiento de la contraseña para consultas posteriores. Asegúrese también de utilizar el dominio de clonación definido durante el proceso de inicialización.
   {: note}

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

	Donde la sintaxis es:

	```
	partition create -partition <nombre-nueva-partición>
	```

5.	Confirme que se ha creado la nueva partición:

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

	La salida del mandato `Partition List` ahora muestra seis particiones.
