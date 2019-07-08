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

# 启用 FIPS 140-2（可选）
{: #enable-fips-140-2-optional-}

FIPS（联邦信息处理标准）是一套标准，用于指定实施加密硬件和软件时的安全要求。FIPS 于 1994 年颁布，2001 年发布了对此标准的更新，称为 FIPS 140-2。

如果您需要确保 Hardware Security Module (HSM) 兼容且符合依据 FIPS 运行的机构和政府的要求，那么可以启用 FIPS 140-2 安全算法。此部分提供了有关如何启用此算法的指示信息。

1. 首先，使用 `hsm show` 命令确认当前是否禁用了 FIPS 方式。

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

	输出指出 `The HSM is NOT in FIPS 140-2 approved operation mode`，这确认设备并未运行 FIPS。

2. 使用 `hsm showpolicies` 命令启用 FIPS 方式之前，请查看策略。

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

	此输出显示策略 12 (`Allow non-FIPS algorithms`) 设置为 `On`，这意味着当前允许不符合 FIPS 的算法用于 HSM 中的操作。

3. 使用在[初始化](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-)期间指定的密码以 HSM SO/管理员身份登录。

	```
	[jdoe1] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```
	{: screen}

4. 启用 FIPS 140-2 方式。

	要启用 FIPS 方式，必须修改此过程的第 2 步中查看的策略 (`Allow non-FIPS algorithms`)：

	此过程将擦除 HSM 中的所有现有分区。如果已创建分区和对象，请确保查看分区内容和配置，以便在创建新分区时重新创建这些内容和配置。
	{: note}

	使用 `hsm changepolicy` 命令禁用策略 12 以仅允许使用 FIPS 算法：

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

5. 使用 `hsm show` 命令再次确认现在是否启用了 FIPS 方式。

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

	现在，`hsm showpolicies` 命令应该会显示设备在使用基于策略（代码）12 的 FIPS 140-2 方式，并反映出强制实施了 FIPS 140-2 算法：

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
