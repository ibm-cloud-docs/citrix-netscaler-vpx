---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, install

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

# 安裝 IBM Hardware Security Module (HSM) 用戶端軟體
{: #install-the-ibm-hardware-security-module-hsm-client-software}

在這個步驟中，Citrix VPX 將隨著與 HSM 互動所需的軟體和公用程式一起安裝。

此程序中的步驟 1 和 2 是選用的，僅當 `/var` 路徑中遺漏 safenet 目錄及其中的檔案或子資料夾時才需要。需要這些資源，VPX 才能隨用戶端軟體一起安裝，並容許它執行與 HSM 軟體相關聯的公用程式。
{: note}

尋找認證以存取控制入口網站中列在**裝置 > 裝置清單 > 展開 VPX 名稱**下的 NetScaler CLI。

<img src="images/3-VPX-Credentials.png" alt="圖片" style="width: 400px;"/>

本節以及手冊的其餘部分將需要它們。

請注意，本文件中的所有 VPX 指令和輸出都將列出 `netscalername#`（指示 Shell 執行）或 `>`（表示 VPX CLI 本身）。
{: note}

1.	（選用）取得 `safenet_dirs.tar` 檔，並將它傳送至 `/var` 目錄中的 VPX。`safenet_dirs.tar` 檔可以從[這裡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window} 取得。

	您必須登入至 SoftLayer 帳戶才能存取上面的鏈接。
  {: note}

	<img src="images/4-transfer-safenet_dirs.png" alt="圖片" style="width: 600px;"/>

	這個影像顯示 WinSCP 軟體正在將 `safenet_dir.tar` 檔案傳送至 Citrix VPX。

2.	（選用）解壓縮 `tar` 檔：

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

3.	導覽至 `/var/safenet` 目錄並確認資料夾和檔案已傳送：

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	使用 622 版來執行安裝 Script：

	```
	root@IBMADC690867-s6dr# install_client.sh -v 622
	*********************************************
	Current Version: 622
	Installing Version: 622
	Starting to extract SAClient_622.tgz file.
	Extracted SAClient_622.tgz file.
	Removing SAClient_622.tgz file.

	*********************************************

	現在，請遵循在 Citrix edocs 線上提供的配置步驟文件。
	*********************************************
	```

5.	確認建立 safenet 目錄：

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	導覽至 `/var/safenet/config/` 目錄，並執行 `safenet_config` Script：

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	驗證已建立 `/etc/Chrystoki.conf` 和符號鏈結 `/usr/lib/libCrystore_64`：

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

IBM© Hardware Security Module 已順利安裝。
