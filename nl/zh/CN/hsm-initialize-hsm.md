---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, initialize

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

# 初始化 IBM Hardware Security Module (HSM)
{: #initialize-ibm-hardware-security-module-hsm-}

大部分配置需要初始化 HSM 设备。否则，只能执行特定 `show` 命令。

要初始化设备，请执行以下步骤：

1.	通过控制门户网站的**设备 > 设备列表 > 展开 HSM 名称**下列出的凭证，使用 SSH 连接到 IBM© Hardware Security Module 设备。

	或者，可以使用公用密钥认证。有关更多信息，请查看 [Appliance Administration Guide（第 38 页）![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}。

	缺省情况下，通常会启用并允许 SSH 访问。如果使用 SSH 进行连接时遇到问题，请检查基础架构路由和安全性。
  {: note}

2. 执行 `hsm init` 命令：

	```
	[jpmongehsm2] lunash:>hsm init -l jpmonge

	Please enter a password for the HSM Administrator:
	> ********

	Please re-enter password to confirm:
	> ********

	Please enter a cloning domain to use for initializing this HSM:
	> ********

	Please re-enter cloning domain to confirm:
	> ********

	CAUTION:  Are you sure you wish to initialize this HSM?

	Type 'proceed' to initialize the HSM, or 'quit'
		to quit now.
		> proceed
		'hsm init' successful.

	Command Result : 0 (Success)
  	```

	其中，使用的语法为：`hsm init -l <hsmlabel>`

`-l` 参数或标签是用于将标识分配给 HSM 的参数，可以是与业务、管理员或所履行角色相关的任何有意义的文本或描述。HSM 管理员密码将是为 HSM 安全主管 (SO) 指定的密码，实际上是创建和配置加密对象以及对 HSM 环境进行更改所需的概要文件。

最后，克隆域是允许在一组 HSM 中构成对象的共享标识。这通常用于备份和/或 HA。

请参阅 [LunaSH Command Reference Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window}，以获取 HSM CLI 中支持的所有可用命令。
