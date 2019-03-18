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

# 安装 IBM 硬件安全模块 (HSM) 客户机软件
{: #install-the-ibm-hardware-security-module-hsm-client-software}

在此步骤中，Citrix VPX 将随与 HSM 交互所需要的软件和实用程序一起安装。

**注：**此过程中的步骤 1 和 2 是可选的，仅当 `/var` 路径中缺少 safenet 目录及其中的文件或子文件夹时才需要。这些资源是随客户机软件一起安装 VPX 所必需的，并允许 VPX 运行与 HSM 软件关联的实用程序。

查找凭证以访问在控制门户网站中**设备 > 设备列表 > 展开 VPX 名称**下列出的 NetScaler CLI。

<img src="images/3-VPX-Credentials.png" alt="图样" style="width: 400px;"/>

本部分和指南的剩余部分将需要这些信息。

**注：**请注意，本文档中的所有 VPX 命令和输出都将列出 `netscalername#`（指示 shell 执行）或 `>`（表示 VPX CLI 本身）。

1.	（可选）获取 `safenet_dirs.tar` 文件，并将其传输到 `/var` 目录中的 VPX。可以从[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window} 获取 `safenet_dirs.tar` 文件。

	**注：**您必须登录到 SoftLayer 帐户才能访问上面的链接。

	<img src="images/4-transfer-safenet_dirs.png" alt="图样" style="width: 600px;"/>

	此图显示了用于将 `safenet_dir.tar` 文件传输到 Citrix VPX 的 WinSCP 软件。

2.	（可选）解压缩 `tar` 文件：

	```
	root@IBMADC690867-wnzs# tar -xvpf safenet_dirs.tar
	x safenet/
	x safenet/config/
	x safenet/gateway/
	x safenet/SAClient_600.tgz
	x safenet/SAClient_622.tgz
	x safenet/install_client.sh
	x safenet/gateway/start_safenet_gw
	x safenet/gateway/gw_delay
	x safenet/config/safenet_config
	x safenet/config/Chrystoki.conf
	```

3.	浏览至 `/var/safenet` 目录，并确认文件夹和文件是否已传输：

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	使用 V622 执行安装脚本：

	```
	root@IBMADC690867-s6dr# install_client.sh -v 622
	*********************************************
	Current Version: 622
	Installing Version: 622
	Starting to extract SAClient_622.tgz file.
	Extracted SAClient_622.tgz file.
	Removing SAClient_622.tgz file.

	*********************************************

	Now follow the configuration steps document available online on Citrix edocs.
	*********************************************
	```

5.	确认 safenet 目录是否已创建：

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	浏览至 `/var/safenet/config/` 目录，并执行 `safenet_config` 脚本：

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	验证 `/etc/Chrystoki.conf` 和符号链接 `/usr/lib/libCrystoki_64` 是否已创建：

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

“IBM© 硬件安全模块”已成功安装。
