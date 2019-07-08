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

# Ativar o FIPS 140-2 (Opcional)
{: #enable-fips-140-2-optional-}

O FIPS (Federal Information Processing Standards) é um conjunto de padrões para especificar requisitos de segurança ao implementar hardware e software criptográfico. Foi criado em 1994 e, em 2001, foi liberada uma atualização para esse padrão conhecida como FIPS 140-2.

Os algoritmos de segurança do FIPS 140-2 podem ser ativados se for necessário garantir que o Hardware Security Module (HSM) seja compatível e esteja em conformidade com agências e governos que operam sob o FIPS. Esta seção fornece instruções sobre como fazer isso.

1. Primeiro, confirme se o modo FIPS está desativado atualmente usando o comando `hsm show`.

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

	A saída declara `The HSM is NOT in FIPS 140-2 approved operation mode`, confirmando que o dispositivo não está executando o FIPS.

2. Revise suas políticas antes de ativar o modo FIPS com o comando `hsm showpolicies`.

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[OUTPUT OMITTED]

	As políticas a seguir são configuradas devido à configuração atual desse HSM e não podem ser mudadas diretamente pelo usuário.

	Description                              Value
	===========                              =====

	PIN-based authentication                  True

	As políticas a seguir descrevem a configuração atual desse HSM e podem ser mudadas pelo administrador do HSM.

	Mudar políticas marcadas como "destrutivas" voltará todo o HSM ao zero (apagará completamente).

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

	Esta saída mostra que a política 12 (`Allow non-FIPS algorithms`) está configurada como `On`, o que significa que os algoritmos que não estão em conformidade com o FIPS são permitidos atualmente para operações no HSM.

3. Efetue login como um sistema operacional/administrador HSM por meio da senha especificada durante a [inicialização](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-).

	```
	[jdoe1] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```
	{: screen}

4. Ativar o modo FIPS 140-2.

	Para ativar o modo FIPS, deve-se modificar a política revisada na etapa dois deste procedimento (`Allow non-FIPS algorithms`):

	Esse procedimento apagará todas as partições existentes no HSM. Se você já criou partições e objetos, certifique-se de revisar o conteúdo e as configurações da partição para recriá-los quando as novas partições forem criadas.
	{: note}

	Use o comando `hsm changepolicy` para desativar a política 12 e permitir somente o uso de algoritmos FIPS:

	```
	[jdoe1] lunash:>hsm changepolicy -policy 12 -value 0

	CUIDADO: tem certeza de que deseja mudar a política destrutiva denominada:

	Allow non-FIPS algorithms

	Mudar essa política resultará no apagamento de todas as partições do HSM. O administrador do HSM, o domínio e M e N (onde aplicável) não serão modificados.

	Digite 'proceed' para voltar seu HSM ao zero e mudar a política ou 'quit' para sair agora.

	> proceed

	'hsm changePolicy' successful.

	A política Allow non-FIPS algorithms está agora configurada para o valor: 0

	Command Result : 0 (Success)
	```
	{: screen}

5. Agora, confirme que o modo FIPS está ativado novamente usando o comando `hsm show`.

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

	O comando `hsm showpolicies` agora deve mostrar que o dispositivo está usando o modo FIPS 140-2 na política (código) 12 e reflete a aplicação dos algoritmos FIPS 140-2:

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[OUTPUT OMITTED]

	As políticas a seguir são configuradas devido à configuração atual desse HSM e não podem ser mudadas diretamente pelo usuário.

	Description                              Value
	===========                              =====
	PIN-based authentication                 True

	As políticas a seguir descrevem a configuração atual desse HSM e podem ser mudadas pelo administrador do HSM. Mudar políticas marcadas como "destrutivas" voltará todo o HSM ao zero (apagará completamente).

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
