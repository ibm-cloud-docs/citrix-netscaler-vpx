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

# SSL 인증서 주문
{: #order-an-ssl-certificate}

SSL(Secure Sockets Layer)은 애플리케이션과 서버 애플리케이션 간의 트래픽을 암호화하는 기술이며 SSL 인증서를 사용하는 공개 키/개인 키 시스템 시스템을 통해 수행됩니다.

SSL 인증서에는 서버의 공개 키, 인증서가 유효한 날짜, 인증서가 유효한 호스트 이름 및 인증서를 발행한 인증 기관의 서명이 포함됩니다.

IBM© Cloud는 서드파티 공급업체/사이트를 통하지 않고도 확보하고 구매할 수 있는 인증서를 제공합니다. 

IBM Cloud는 고객을 위해 1년 및 2년에 한 번씩 SSL 인증서를 제공하며 다음을 포함한 여러 이점이 제공됩니다.

* 비즈니스 ID 및 도메인 소유권 확인을 위한 전체 인증
* 모든 온라인 트랜잭션의 40비트에서 256비트까지의 암호화
* 사이트 및 고객이 보호되는지 확인하는 웹 사이트 및 악성코드의 일일 스캐닝

다중 도메인을 실행 중인 경우 각 도메인에 대한 SSL 인증서를 구매할 수 있습니다.

SSL 인증서에 대한 자세한 정보는 다음 IBM Cloud 기사를 참조하십시오.

* [SSL 인증서 정보](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [SSL 기술 소개](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [SSL을 위한 계획](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)

Citrix Netscaler VPX에 사용할 SSL 인증서를 주문하려면 다음 프로시저를 수행하십시오.

1.	VPX 쉘 CLI의 [키 작성 및 인증서 서명 요청(CSR) 생성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) 단계에서 이전에 작성한 CSR 파일을 열어 CSR 텍스트를 표시하십시오.

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

2.	`---BEGIN NEW CERTIFICATE REQUEST---`에서 `---END NEW CERTIFICATE REQUEST---`까지 파일의 컨텐츠를 복사하십시오.

3.	적절한 필드에서 CSR 파일 텍스트를 붙여넣어 [이 지시사항](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates)을 따라 주문하십시오. 다음 예제에서 `RapidSSL 1 Year`이 선택되었습니다.

	<img src="images/5-Order-Certificate_1.png" alt="그림" style="width: 550px;"/>

	표시된 대로 시스템이 CSR 텍스트를 처리하고 해석한 후 이를 다음 페이지에 표시합니다.

	도메인의 소유권을 유효성 검증하기 위해 지정된 방법인 유효한 이메일 계정 및 도메인/하위 도메인을 선택해야 합니다.

	주문 세부사항을 확인하고 **주문하기**를 클릭하십시오.

4. 사용자가 표시한 계정에 대한 인증서 요청의 세부사항이 포함된 주문 확인이 수신됩니다.

	이메일에서 괄호 안의 링크를 클릭하여 도메인 유효성 검증 요청을 승인하십시오. 이제 SSL 요청의 수행 준비가 되었습니다. 
