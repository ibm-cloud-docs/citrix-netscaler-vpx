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

# 建立网络信任链路 (NTL)
{: #establish-a-network-trust-link-ntl-}

网络信任链路 (NTL) 是硬件安全模块 (HSM) 与客户机进行通信的安全通道。NTL 使用双向证书来认证和加密在 HSM 服务器分区与客户机之间传输的数据。

请注意，信任链路需要在 NTLS 和 NTLA（双向）协议中都可访问 TCP 端口 1792，才可保证所有进程和实用程序都能正常工作。

要建立 NTL，请执行以下过程：

1.	浏览至 `/var/safenet/safenet/lunaclient/bin` 目录，然后使用 VTL 实用程序创建证书。

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	Private Key created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	Certificate created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**注：**用于客户机证书的标识是为其分配的专用 IP。此 IP 稍后会被 HSM 使用和引用。

2. 使用 SCP 将证书文件传输到 HSM 服务器：

	```
	root@IBMADC690867-s6dr# scp /var/safenet/safenet/lunaclient/cert/client/	10.121.229.224.pem hsm_admin@10.121.229.201:

	The authenticity of host '10.121.229.201 (10.121.229.201)' can't be established.

	ECDSA key fingerprint is SHA256:UBltOfaDojRlUVxDXh6zI3CPMF8FRaJnls0uxeWgrCY.

	Are you sure you want to continue connecting (yes/no)? yes

	Warning: Permanently added '10.121.229.201' (ECDSA) to the list of known hosts.

	hsm_admin@10.121.229.201's password:

	10.121.229.224.pem                                                 
	100%  818     	
	1.6MB/s   
	00:00
	```

	要了解有关虚拟令牌库 (VTL) 的更多信息，请转至 [Utilities Reference Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}。

3.	使用 SCP 将 HSM 服务器证书文件传输到 Citrix Netscaler VPX 客户机，然后添加服务器：

	```
	root@IBMADC690867-s6dr# scp hsm_admin@10.121.229.201:server.pem .
	hsm_admin@10.121.229.201's password:

	server.pem                                                         
	100% 1180     	
	2.3MB/s   
	00:00

	root@IBMADC690867-s6dr# vtl addServer -n 10.121.229.201 -c server.pem

	New server 10.121.229.201 successfully added to server list.
	```

	上面使用的语法如下：

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. 确认服务器是否已添加：

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	在 HSM 中，执行以下命令以查看任何现有客户机：

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs

	Command Result : 0 (Success)
	```

5.	将 VPX 注册为新客户机：

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	'client register' successful.

	Command Result : 0 (Success)
	```

	上面的命令使用以下语法：

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	客户机名称不必与 IBM© Cloud 所分配和使用的标识相匹配，但是建议使名称保持一致。

6. 确认客户机是否已添加：

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs
	registered client 6: NS-IBMADC690867-s6dr

	Command Result : 0 (Success)
	```

7. 为客户机分配分区。确保引用了先前创建的分区。您还必须确保该名称与上一步中显示的客户机的标识相匹配。

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition' successful.

	Command Result : 0 (Success)
	```

	上面的输出使用以下语法：

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	验证 Citrus NetScaler VPX 的连接：

	```
	root@IBMADC690867-s6dr# vtl verify

	The following Luna SA Slots/Partitions were found:

	Slot    Serial #                Label
	====    ================        =====
	0           534071053        partition6
	```

	`vtl verify` 显示的输出应该会列出分区的“插槽号”、序列号和绑定到此信任链路的分区的名称。其他任何输出都指示有问题。

	此外，最好在 `/etc` 目录下的 Chrystoki 文件中确认证书和服务器的路径。为此，请执行以下操作：

	```
	root@IBMADC690867-s6dr# cd /etc/
	root@IBMADC690867-s6dr# cat /etc/Chrystoki.conf
	Chrystoki2 = {
		LibUNIX64 = /var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so;
		}

	[OUTPUT OMMITED]
		ClientPrivKeyFile = /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem;
		ClientCertFile = /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem;
		ServerCAFile = /var/safenet/safenet/lunaclient/cert/server/CAFile.pem;
		NetClient = 1;
		HtlDir = /var/safenet/safenet/lunaclient/htl/;
		ServerName00 = 10.121.229.201;
		ServerPort00 = 1792;
		ServerHtl00 = 0;
	}
	[OUTPUT OMITTED]
	```

9.	保存配置：

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	此处使用的复制命令可使配置在 VPX 中的重新引导过程中持久存储。

10.	启动加密操作所需的 SafeNet 网关客户机进程：

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. 确认进程是否正在运行：

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. 最后，确保在重新引导过程中自动启动此进程：

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

现在，NTL 已建立。
