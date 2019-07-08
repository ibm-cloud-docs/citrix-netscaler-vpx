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

# 创建分区
{: #create-a-partition}

分区是一种逻辑独立空间，与向 HSM 引擎请求加密对象或在 HSM 引擎中创建加密对象的客户机请求相关联或连接。每个分区都有自己的数据和策略，与其他分区相隔离。要了解有关分区的更多信息，请参阅 [Administration Guide（第 211 页）![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}。

要创建分区，请执行以下过程：

1.	在[初始化](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-)期间，以 HSM 安全主管/管理员身份使用指定的密码登录：

	```
	[jpmongehsm2] lunash:>hsm login

	Please enter the HSM Administrators' password:
	> ********

	'hsm login' successful.

	Command Result : 0 (Success)
	```

2.	确认 HSM Admin Login Status 是否为“Logged In”：

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

	以上输出应该在 HSM Admin login status 中显示 `Logged In`。否则，在以下各部分中列出的大多数操作和命令都会失败，因为这些操作和命令需要管理员访问权。

3.	列出所有现有分区：

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

	此输出显示五个现有分区。

4.	创建新分区：

	 此步骤中定义的密码稍后将用于在 Citrix VPX HSM 客户机进程中关联和创建对象。请记录此密码以供未来引用。另外，请确保使用初始化过程中定义的克隆域。
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

	其中语法为：

	```
	partition create -partition <name-for-new-Partition>
	```

5.	确认新分区是否已创建：

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

	`Partition List` 命令的输出现在显示六个分区。
