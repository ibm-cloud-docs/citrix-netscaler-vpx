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

# 訂購 SSL 憑證
{: #order-an-ssl-certificate}

Secure Sockets Layer (SSL) 是一種可在用戶端應用程式與伺服器應用程式之間加密資料流量的技術，它透過使用 SSL 憑證的公開金鑰/私密金鑰系統來完成。

SSL 憑證包含伺服器的公開金鑰、憑證的有效日期、憑證的有效主機名稱，以及簽發該憑證的憑證管理中心簽章。

IBM© Cloud 提供可獲得並購買的憑證，不必透過第三方供應商/網站進行。

IBM Cloud 為客戶提供每年及每半年的 SSL 憑證，憑證提供各種優點，包括：

* 商業身分及網域所有權驗證的完整鑑別
* 所有線上交易的 40 到 256 位元加密
* 每日進行網站的惡意軟體掃描，確保您的網站與客戶都受到保護

如果您經營多個網域，可以為每個網域購買 SSL 憑證。

如需 SSL 憑證的相關資訊，請參閱下列 IBM Cloud 文章：

* [關於 SSL 憑證](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [SSL 技術簡介](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [規劃 SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)


若要訂購 SSL 憑證以搭配 Citrix Netscaler VPX 使用，請執行下列程序：

1.	在 VPX Shell CLI 中，開啟先前在步驟[建立金鑰並產生憑證簽署要求 (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-)中建立的 CSR 檔案，以顯示 CSR 文字：

	```
	root@IBMADC690867-s6dr# cat certreqnss6dr.csr
	-----BEGIN NEW CERTIFICATE REQUEST-----
	MIIC5jCCAc4CAQAwgaAxCzAJBgNVBAYTMRcwFQYDVQQIEw5Ob3J0aCBDYXJv
	bGluYTEPMA0GA1UEBxMGRHVyaGFtMQwwCgYDVQQKEwNJQk0xDDAKBgNVBAsTA0hT
	TTEoMCYGA1UEAxMfaHNW50Ny5wcm9qZWN0Z29sZGZpbmNoLm5ldDEhMB8G
	CSqGSIb3DQEJARYSanBtb25nZUBjci5pYm0uY29tMIIBIjANBgkqhkiG9w0BAQEF
	/pXQN+a55HhWmnyj5gThAprOoN8DeiVN+1HI+PA+g1
	r4+8dKA1xz+jPhWDQgQYb3Wnh8VK8Ouids6uFnsoc3KDymbzoWZYctp8PA6uBzJ/
	25RGiZquRu9MYJIWkQ46WQ14PoJ8BiYuJa/N6L47+Jr2vaCntmXBU4rFrjctHqq8
	Hct9q5OVYXbYLQB+MM3gYyyFBQpZ1sHZD4D6K3AISRGsOE9rrovGjUfO8mLKE6a
	AQEFBQADggEBAMe+kmdPNtt8LOpaAy+u5i9GpgHfH5zW2sX4Lj7srkqwmyxavqjE
	XvM9PPudXV9OCUWewtlm/Eqo1pYIRudFBrjg5UJyKpM4sWWdKIrTk8RZusdOUvKU
	0vBRJRJ3Yy/1olXFO05FFSotAyB9P5v9siMwdWUhM9pSiGwoNXCB74m2sxgUh10J
	H0IvDl3SL4ptosV10KJtbOiO/YV9XXNaW8/X/2uM9Y3stcnSvzJGrFlPmbhK7Vsd
	uL6/wSnV1E70CDT+KPPapzVJr/S8nP5xHVVl/5/JUGZa8rx01g9EBmX36H3T
	kHD85XOkSI4y04Y3t6pMVbIAz0vipOmHYlM=
	-----END NEW CERTIFICATE REQUEST-----
	```

2.	複製檔案的內容，從 `---BEGIN NEW CERTIFICATE REQUEST---` 開始一直到 `---END NEW CERTIFICATE REQUEST---`。

3.	遵循[這些指示](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates)來下訂單，並在適當的欄位中貼上 CSR 檔案文字。在下列範例中，已選擇 `RapidSSL 1 Year`。

	<img src="images/5-Order-Certificate_1.png" alt="圖片" style="width: 550px;"/>

	如顯示，系統會處理並解譯 CSR 文字，然後在接下來的頁面顯示。

	請務必選取有效的電子郵件帳戶及網域/子網域，因為這是用來驗證網域所有權的指定方法。

	確認訂單詳細資料，然後按**下訂單**。

4. 您將收到一份訂單確認，其中含有您所指出帳戶之憑證要求的詳細資料。

	按一下電子郵件中含括的鏈結，以核准網域驗證要求。此時，SSL 要求應該可以開始履行。
