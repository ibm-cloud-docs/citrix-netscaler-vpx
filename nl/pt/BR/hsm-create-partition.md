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

# Criar uma Partição
{: #create-a-partition}

Uma partição é um espaço lógico e independente que está associado ou conectado ao cliente que está solicitando ou criando objetos criptográficos no mecanismo do HSM. Cada partição tem seus próprios dados e políticas isolados de outras partições. Para saber mais sobre partições, consulte o [Guia de Administração (página 211) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}.

Para criar uma partição, execute o procedimento a seguir:

1.	Efetue login como o responsável pela segurança/administrador do HSM usando a senha especificada durante a [inicialização](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-):

	```
	[jpmongehsm2] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```

2.	Confirme se o status do login do administrador do HSM é “Login efetuado”:

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

	A saída acima deve mostrar `Logged In` no status de login do administrador do HSM. Caso contrário, a maioria das operações e comandos listados nas seções a seguir falharão conforme precisarem de acesso de administrador.

3.	Liste qualquer partição existente:

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

	Esta saída mostra cinco partições existentes.

4.	Crie uma nova partição:

	**NOTA:** a senha definida nessa etapa será usada posteriormente para associar e criar objetos no processo do cliente de gerenciamento de armazenamento hierárquico do Citrix VPX. Mantenha o controle dessa senha para referência posterior. Além disso, certifique-se de usar o domínio de clonagem definido durante o processo de inicialização.

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

	Em que a sintaxe é:

	```
	partition create -partition <name-for-new-Partition>
	```

5.	Confirme se a nova partição foi criada:

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

	A saída do comando `Partition List` agora mostra seis partições.
