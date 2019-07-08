---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, keys, csr

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

# 建立金鑰並產生憑證簽署要求 (CSR)
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

在這個子節中，我們將建立一個金鑰組，以用來產生「憑證簽章要求 (CSR)」，並用它訂購/要求憑證。

1.	首先，確認 VPX 中的物件清單。在建立期間，針對此分割區使用指定的密碼。

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	```

	此輸出會確認沒有物件存在，因為輸出為空白/空的。

	然後顯示分割區詳細資料，驗證 HSM 中的物件計數為 0：

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

	上面列出的指令使用下列語法：

	```
	partition show -p <partition_name>
	```

2.	在 VPX 中使用「憑證管理公用程式 (CMU)」，使用下面顯示的指令建立金鑰組。請再次使用指定的分割區密碼。

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	Select RSA Mechanism Type - 
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	在上述語法中，`modulusBits` 參數指出 RSA 金鑰的長度（以位元為單位），而 `publicExponent` 會定義用於產生金鑰的公開指數值，這必須設為 3、17 或 65537。label 關鍵字用於指定標籤，以方便之後參照和識別。如需其他兩個/其他參數的相關資訊，請參閱 [Utilities Reference Guide ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}。

3.	確認已建立物件。在 VPX 中：

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

4.	使用前一個步驟中建立的金鑰，以 CMU 公用程式來產生 CSR。

	請務必針對「通用名稱 (CN)」及「電子郵件 (E)」使用正確/適當的值，第一個值應該符合與虛擬伺服器/IP (VPX) 相關聯之 DNS A 記錄中將使用的 FQDN。在要求/訂購此項目之後，E 參數將用來傳送憑證採購詳細資料。

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

	在上述輸出中，檔名可以是具有 .csr 副檔名的任何名稱，不過，建議您使用有意義的說明。

5.	確認檔案的建立

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
