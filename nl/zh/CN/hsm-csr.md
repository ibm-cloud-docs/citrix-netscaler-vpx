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

# 创建密钥并生成证书签名请求 (CSR)
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

在此子节中，我们将创建一个密钥对，用于生成证书签名请求 (CSR) 并使用该请求来订购/请求证书。

1.	首先，确认 VPX 中的对象列表。在创建期间使用此分区的指定密码。

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : 	********** 
	```

	此输出确认不存在任何对象，因为输出为空白/为空。

	然后，通过显示分区详细信息来验证 HSM 中的对象计数是否为 0：

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	Partition Name:                            partition6
	Partition SN:                              534071053
	Partition Label:                           partition6
	Partition Owner Locked Out:                no
	Partition Owner PIN To Be Changed:         no
	Partition Owner Login Attempts Left:       10 before Partition Owner is Locked Out
	Legacy Domain Has Been Set:                no
	Partition Storage Information (Bytes):     Total=207559, Used=0, Free=207559
	Partition Object Count:                    0

	Command Result : 0 (Success)
	```

	上面列出的命令使用以下语法：

	```
	partition show -p <partition_name>
	```

2.	通过 VPX 中的证书管理实用程序 (CMU)，使用下面显示的命令来创建密钥对。再次使用指定的分区密码。

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	Select RSA Mechanism Type - 
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	在上面的语法中，`moduleusBits` 参数指示 RSA 密钥的长度，`publicExponent` 定义要用于生成密钥的公共指数值，此值必须设置为 3、17 或 65537。“label”关键字用于指定一个标记，以供稍后轻松引用和识别。有关其他两个/更多参数的更多信息，请查看 [Utilities Reference Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}。

3.	确认对象是否已创建。在 VPX 中：

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	在 HSM 中：

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	Partition Name:                            partition6
	Partition SN:                              534071053
	Partition Label:                           partition6
	Partition Owner Locked Out:                no
	Partition Owner PIN To Be Changed:         no
	Partition Owner Login Attempts Left:       10 before Partition Owner is Locked Out
	Legacy Domain Has Been Set:                no
	Partition Storage Information (Bytes):     Total=207559, Used=1660,  Free=205899
	Partition Object Count:                    2

	Command Result : 0 (Success)
	```

4.	使用上一步中创建的密钥通过 CMU 实用程序生成 CSR。

	确保使用公共名称 (CN) 和电子邮件 (E) 的正确/适当值，CN 应该匹配将在与虚拟服务器/IP (VPX) 关联的 DNS A 记录中使用的 FQDN。E 参数将用于在请求/订购证书后发送证书购买详细信息。

	```
	root@IBMADC690867-s6dr# cmu requestcertificate

	Please enter password for token in slot 0 : **********

	Enter Subject 2-letter Country Code (C) : US
	Enter Subject State or Province Name (S) : North Carolina
	Enter Subject Locality Name (L) : Durham
	Enter Subject Organization Name (O) : IBM
	Enter Subject Organization Unit Name (OU) : HSM
	Enter Subject Common Name (CN) : hsmclient7.projectgoldfinch.net   
	Enter EMAIL Address (E) : user@yourdomain.com
	Enter output filename : certreqnss6dr.csr
	```

	在上面列出的输出中，文件名可以是具有 .csr 扩展名的任何名称，但是建议使用有意义的描述。

5.	确认文件是否已创建。

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
