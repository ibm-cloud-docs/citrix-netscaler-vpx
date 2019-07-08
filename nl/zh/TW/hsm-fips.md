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

# 啟用 FIPS 140-2（選用）
{: #enable-fips-140-2-optional-}

FIPS（聯邦資訊處理標準）是一套標準，用於指定實作加密硬體和軟體時的安全要求。FIPS 於 1994 年頒佈，2001 年發佈了對此標準的更新，稱為 FIPS 140-2。

如果您需要確保 Hardware Security Module (HSM) 相容且符合依據 FIPS 運行的機構和政府的要求，則可以啟用 FIPS 140-2 安全演算法。此區段提供了啟用此安全演算法的指示。

1. 首先，使用 `hsm show` 指令確認目前是否停用了 FIPS 模式。

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

	輸出指出 `The HSM is NOT in FIPS 140-2 approved operation mode`，確認裝置未執行 FIPS。

2. 使用 `hsm showpolicies` 指令啟用 FIPS 模式之前，請先檢閱原則。

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[輸出省略]

	The following policies are set due to current configuration of this HSM and cannot be altered directly by the user.

	Description                              Value
	===========                              =====

	PIN-based authentication                  True

	下列原則說明此 HSM 的現行配置，且可以由 HSM 管理者變更。

	變更標示為"destructive" 的原則會將整個 HSM 化零（完全消除）。

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

	此輸出顯示原則 12 (`Allow non-FIPS algorithms`) 設為 `On`，這意味著目前容許不符合 FIPS 的演算法用於 HSM 中的作業。

3. 使用在[起始設定](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-)期間指定的密碼以 HSM SO/管理員身分登入。

	```
	[jdoe1] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```
	{: screen}

4. 啟用 FIPS 140-2 模式。

	若要啟用 FIPS 模式，必須修改此程序的步驟 2 中檢閱的原則 (`Allow non-FIPS algorithms`)：

	此程序將消除 HSM 中的所有現有分割區。如果已建立分割區和物件，請確保檢閱分割區內容和配置，以便在建立新分割區時重建這些內容和配置。
	{: note}

	使用 `hsm changepolicy` 指令來停用原則 12 並僅容許使用 FIPS 演算法：

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

5. 使用 `hsm show` 指令再次確認現在是否已啟用了 FIPS 模式。

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

	現在，`hsm showpolicies` 指令應該會顯示裝置在使用基於原則（代碼）12 的 FIPS 140-2 模式，並反映出強制實施了 FIPS 140-2 演算法：

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[輸出省略]

	The following policies are set due to current 	configuration of this HSM and cannot be altered directly by the user.

	Description                              Value
	===========                              =====
	PIN-based authentication                  True

	下列原則說明此 HSM 的現行配置，且可以由 HSM 管理者變更。變更標示為"destructive" 的原則會將整個 HSM 化零（完全消除）。

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
