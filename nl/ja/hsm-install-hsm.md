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

# IBM Hardware Security Module (HSM) クライアント・ソフトウェアのインストール
{: #install-the-ibm-hardware-security-module-hsm-client-software}

この手順では、Citrix VPX を、HSM と対話するために必要なソフトウェアおよびユーティリティーと共にインストールします。

**注:** この手順のステップ 1 とステップ 2 はオプションであり、safenet ディレクトリーおよびそのディレクトリーに含まれるファイルまたはサブフォルダーが `/var` パスから欠落している場合にのみ必要となります。 これらのリソースは、VPX をクライアント・ソフトウェアと共にインストールし、HSM ソフトウェアに関連するユーティリティーを VPX で実行できるようにするために必要です。

Control Portal の **「デバイス」>「デバイス・リスト」>「VPX 名の展開 (Expand VPX name)」** の下で、NetScaler CLI にアクセスするための資格情報を見つけます。

<img src="images/3-VPX-Credentials.png" alt="図面" style="width: 400px;"/>

これらは、このセクションおよびガイドの残りの部分で必要になります。

**注:** この文書に記載されているすべての VPX コマンドおよび出力では、`netscalername#` (シェルの実行を示す)、または `>` (VPX CLI 自体) がリストされることに注意してください。

1.	(オプション) `safenet_dirs.tar` ファイルを取得し、`/var` ディレクトリー内の VPX に転送します。 `safenet_dirs.tar` ファイルは、[こちら![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window}から取得できます。

	**注:** 上記のリンクにアクセスするには、SoftLayer アカウントにログインしている必要があります。

	<img src="images/4-transfer-safenet_dirs.png" alt="図面" style="width: 600px;"/>

	この画像は、WinSCP ソフトウェアで `safenet_dir.tar` ファイルを Citrix VPX に転送している状況を示しています。

2.	(オプション) `tar` ファイルを解凍します。

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

3.	`/var/safenet` ディレクトリーにナビゲートし、フォルダーおよびファイルが転送されたことを確認します。

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	バージョン 622 を使用して、インストール・スクリプトを実行します。

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

5.	safenet ディレクトリーが作成されたことを確認します。

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	`/var/safenet/config/` ディレクトリーにナビゲートして、`safenet_config` スクリプトを実行します。

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	`/etc/Chrystoki.conf` およびシンボリック・リンク `/usr/lib/libCrystoki_64` が作成されたことを確認します。

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

IBM© Hardware Security Module が正常にインストールされました。
