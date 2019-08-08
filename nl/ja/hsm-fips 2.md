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

# FIPS 140-2 の有効化 (オプション)
{: #enable-fips-140-2-optional-}

FIPS (連邦情報処理標準) は、暗号化ハードウェアや暗号化ソフトウェアの実装に関するセキュリティー要件を規定した一連の標準です。1994 年に作成され、2001 年に FIPS 140-2 として知られる更新版の標準がリリースされました。

FIPS に準拠して業務を行う自治体や政府機関で、ハードウェア・セキュリティー・モジュール (HSM) の適合性と準拠性を確保する必要がある場合は、FIPS 140-2 セキュリティー・アルゴリズムを有効にしてください。このセクションでは、その手順について説明します。

1. まず、コマンド `hsm show` を使用して、FIPS モードが現在無効になっていることを確認します。

	```
	[jdoe1] lunash:>hsm show

	Appliance Details:
	==================
	Software Version:   6.2.2-5

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

		[出力省略]

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

	デバイスで FIPS が実行されていないことを示す「`The HSM is NOT in FIPS 140-2 approved operation mode.`」(HSM は、FIPS 140-2 認定の動作モードではありません) という出力が表示されています。

2. FIPS モードを有効にする前に `hsm showpolicies` コマンドでポリシーを確認します。

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[出力省略]

	以下のポリシーは、この HSM の現在の構成を基に設定されたものであり、ユーザーが直接変更することはできません。

	Description                              Value
	===========                              =====

	PIN-based authentication                  True

	以下のポリシーは、この HSM の現在の構成を表すものであり、HSM 管理者による変更が可能です。

	「destructive (破壊的)」とマークされたポリシーを変更すると、HSM 全体がゼロ化 (完全に消去) されます。

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

	この出力では、ポリシー 12 (`Allow non-FIPS algorithms` (非 FIPS アルゴリズムを許可する)) が `On` に設定されています。これは、現在、FIPS に準拠していないアルゴリズムが HSM の操作で許可されていることを意味します。

3. [初期化](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-)したときに指定したパスワードを使用して、HSM SO/管理者としてログインします。

	```
	[jdoe1] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```
	{: screen}

4. FIPS 140-2 モードを有効にします。

	FIPS モードを有効にするには、手順 2 で確認したポリシー (`Allow non-FIPS algorithms` (非 FIPS アルゴリズムを許可する)) を変更する必要があります。

	この手順を実行すると、HSM の既存のパーティションがすべて消去されます。既に作成したパーティションとオブジェクトがある場合は、新規パーティションの作成時にそれらを再作成するために、パーティションの内容と構成を確認してください。
	{: note}

	ポリシー 12 を無効にして FIPS アルゴリズムの使用のみを許可するには、`hsm changepolicy` コマンドを使用します。

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

5. もう一度コマンド `hsm show` を使用して、FIPS モードが有効になったことを確認します。

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

	コマンド `hsm showpolicies` を実行すると、今回は、ポリシー (コード) 12 でデバイスが FIPS 140-2 モードを使用していることが表示されます。FIPS 140-2 アルゴリズムの適用が反映されています。

	```
	[jdoe1] lunash:>hsm showpolicies

	HSM Label:   jpmonge
	Serial #:    534071
	Firmware:    6.10.9

	[出力省略]

	以下のポリシーは、この HSM の現在の構成を基に設定されたものであり、ユーザーが直接変更することはできません。

	Description                              Value
	===========                              =====
	PIN-based authentication                 True

	以下のポリシーは、この HSM の現在の構成を表すものであり、HSM 管理者による変更が可能です。「destructive (破壊的)」とマークされたポリシーを変更すると、HSM 全体がゼロ化 (完全に消去) されます。

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
