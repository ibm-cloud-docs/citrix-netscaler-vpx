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

# 建立分割區
{: #create-a-partition}

分割區是一種邏輯且獨立的空間，它關聯於或連接在 HSM 引擎中要求或建立加密物件的用戶端。每一個分割區都有自己與其他分割區隔離的資料和原則。若要進一步瞭解分割區，請參閱 [Administration Guide（第 211 頁）![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}。

若要建立分割區，請執行下列程序：

1.	使用[起始設定](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-)期間指定的密碼，以 HSM Security Officer/Administrator 身分登入：

	```
	[jpmongehsm2] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```

2.	確認 HSM 管理登入狀態是 Logged In：

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

	以上的輸出應該在 HSM 管理登入狀態下顯示 `Logged In`。否則，下列各節所列的大部分作業及指令將會失敗，因為它們需要管理者存取權。

3.	列出任何現有的分割區：

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

	此輸出顯示五個現有的分割區。

4.	建立新的分割區：

	 此步驟中定義的密碼稍後將用於在 Citrix VPX HSM 用戶端處理程序中關聯和建立物件。請記下此密碼，以便之後能夠參考。此外，請務必使用起始設定程序期間所定義的複製網域。
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

	其中語法為：

	```
	partition create -partition <name-for-new-Partition>
	```

5.	確認已建立新的分割區：

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

	`Partition List` 指令的輸出現在顯示六個分割區。
