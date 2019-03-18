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

# 安裝 SSL 憑證
{: #install-your-ssl-certificate}

在本主題中，您將安裝您在前一個[逐步作業](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx)中建立的 SSL 憑證。若要這樣做，請執行下列程序：

1.	確認憑證位於 Citrix Netscaler VPX 的 `/nsconfig/ssl` 目錄中。

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	即使憑證金鑰位於適當的目錄中，也必須將它辨識為有效的 Citrix Netscaler VPX 物件，讓它連接其他 VPX 元件並與其互動。若要這麼做，請執行下列動作：

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	ERROR:  Internal error while adding HSM key.
	```

	上一個指令使用下列語法：

	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	其中 `keyName` 是在 IBM© Hardware Security Module (HSM) 上使用 CMU 公用程式建立的金鑰名稱。`serialNum` 參數是相關分割區的序號。`password` 參數，如同之前一樣是金鑰所在分割區的密碼。

	**附註：**預期會有 `Internal error` 訊息，因為完成此步驟所花的時間增加。應該已適當地新增金鑰。不過，您收到的任何其他錯誤訊息都應該解決。

3.	確認已新增金鑰：

	```
	> show ssl hsmkey
	1) HSM Key Name: NSkey_s6dr
 	Done
	```

4.	如同 HSM 金鑰，必須使用適當的 Citrix VPX 指令來新增 SSL 憑證，才能辨識它：

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	Done
	```

	上述指令的使用語法如下：

	```
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	其中 `certkey` 是要在 VPX 裝置中新增的憑證物件名稱。`cert` 參數包含檔案的名稱及路徑（如果它位於非現行目錄的目錄）。最後，`hsmkey` 包含前一個步驟中新增的金鑰名稱。

5.	確認已安裝憑證：

	```
	> show ssl certKey
	[OUTPUT OMITTED]
		2) Name: hsmclient7ns
		Cert Path: /nsconfig/ssl/hsmclient7.cer
		HSM Key ID: NSkey_s6dr
		Format: PEM
		Status: Valid,   Days to expiration:350
		Certificate Expiry Monitor: ENABLED
		Expiry Notification period: 30 days
		Certificate Type: "Client Certificate" "Server Certificate"
		Version: 3
		Serial Number: 01785B2B61C8D7F1C06AC7CA8EDD573D
		Signature Algorithm: sha256WithRSAEncryption
		Issuer:  C=US,O=DigiCert
	Inc,OU=www.digicert.com,CN=RapidSSL RSA CA 2018
		Validity
			Not Before: Jul 26 00:00:00 2018 GMT
			Not After : Jul 26 12:00:00 2019 GMT
		Subject:  CN=hsmclient7.projectgoldfinch.net
		Public Key Algorithm: rsaEncryption
		Public Key size: 2048
		Ocsp Response Status: NONE
	[OUTPUT OMITTED]
	Done
	>
	```

6.	（選用）若要避免在透過 Web 瀏覽器存取內容時發生安全警告，建議您安裝「中間 CA」憑證。這些選項可讓 Citrix Netscaler VPX 與連接的用戶端共用資訊。

	若要為 RapidSSL 取得這些中繼憑證，請造訪下列任一鏈結：

	* [Reissue GeoTrust Certificate For Partner Orders or QuickSSL ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [RapidSSL Intermediate and Root CA Certificates ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	若要安裝及鏈結憑證，請遵循這篇 [Citrix 文章 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://support.citrix.com/article/CTX114146){:new_window}。

	```
	> show ssl certlink
	1) Cert Name: hsmclient7ns  CA Cert Name: ICARSSL
	Done
	```
