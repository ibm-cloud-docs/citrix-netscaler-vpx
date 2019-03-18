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

# SSL 인증서 설치
{: #install-your-ssl-certificate}

이 주제에서는 이전 [단계별](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) 지시사항에서 작성된 SSL 인증서를 설치합니다. 이를 수행하려면 다음 프로시저를 따르십시오.

1.	인증서가 Citrix Netscaler VPX의 `/nsconfig/ssl` 디렉토리에 있는지 확인하십시오.

	```
	root@IBMADC690867-s6dr# cd /nsconfig/ssl
	root@IBMADC690867-s6dr# ls
	certbundle              ns-root.srl             ns-	sftrust-root.key     ns-sftrust.key
	hsmclient7.cer          ns-server.cert          ns-	sftrust-root.req     ns-sftrust.req
	ns-root.cert            ns-server.key           ns-	sftrust-root.srl     ns-sftrust.sig
	ns-root.key             ns-server.req           ns-	sftrust.cert
	ns-root.req             ns-sftrust-root.cert    ns-	sftrust.der
	```

2.	인증서 키가 적절한 디렉토리에 위치한 경우에도 기타 VPX 컴포넌트와 상호 작용하고 이 VPX 컴포넌트에 연결되도록 유효한 Citrix Netscaler VPX 오브젝트로 인식되어야 합니다. 이를 위해 다음을 수행하십시오.

	```
	> add ssl hsmKey NSkey_s6dr -hsmType SAFENET -	SerialNum 534071053 -password P@rtition6
	오류: HSM 키를 추가하는 중에 내부 오류가 발생했습니다.
	```

	이전 명령에서 다음 구문을 사용합니다.

	```
	add ssl hsmkey <KeyName> -hsmType SAFENET -serialNum 	<serial #> -password <password>
	```

	여기서, `keyName`은 CMU 유틸리티를 사용하여 IBM© Hardware Security Module(HSM)에 작성된 키의 이름입니다. `serialNum` 매개변수는 문제가 되는 파티션의 일련 번호입니다. `password` 비밀번호는 이전과 같이 키가 존재하는 파티션의 비밀번호입니다.

	**참고:** `Internal error` 메시지는 이 단계를 완료하는 데 걸리는 시간이 증가함에 따라 표시됩니다. 키는 올바르게 추가되어야 합니다. 그러나 수신된 기타 오류 메시지는 처리되어야 합니다.

3.	키가 추가되었는지 확인하십시오.

	```
	> show ssl hsmkey
	1) HSM 키 이름: NSkey_s6dr
 	완료
	```

4.	HSM 키와 같이 SSL 인증서는 인식될 적절한 Citrix VPX 명령을 사용하여 추가되어야 합니다.

	```
	> add ssl certkey hsmclient7ns -cert /nsconfig/ssl/	hsmclient7.cer -hsmkey NSkey_s6dr
	완료
	```

	위의 명령의 경우 다음 구문이 사용됩니다.

	```
	add ssl certkey <CertkeyName> -cert <cert path/name>
	-hsmkey <KeyName>
	```

	여기서, `certkey`는 VPX 디바이스에 사용될 인증서 오브젝트의 이름입니다. `cert` 매개변수가 현재 디렉토리 이외의 디렉토리에 위치한 경우 파일에 대한 이름 및 경로를 포함합니다. 마지막으로 `hsmkey`에는 이전 단계에 추가된 키의 이름이 포함됩니다.

5.	인증서가 설치되었는지 확인하십시오.

	```
	> show ssl certKey
	[출력이 생략됨]
		2) 이름: hsmclient7ns
		인증서 경로: /nsconfig/ssl/hsmclient7.cer
		HSM 키 ID: NSkey_s6dr
		형식: PEM
		상태: 유효함,    만기까지 남은 날짜: 350
		인증서 만기 모니터: ENABLED
		만기 알림 기간: 30일
		인증서 유형: "클라이언트 인증서" "서버 인증서"
		버전: 3
		일련 번호: 01785B2B61C8D7F1C06AC7CA8EDD573D
		시그니처 알고리즘: sha256WithRSAEncryption
		발행자:  C=US,O=DigiCert
	Inc,OU=www.digicert.com,CN=RapidSSL RSA CA 2018
		유효성
			시작일: 2018년 7월 26일 00:00:00 GMT
			종료일: 2019년 7월 26일 12:00:00 GMT
		주제:  CN=hsmclient7.projectgoldfinch.net
		공개 키 알고리즘: rsaEncryption
		공개 키 크기: 2048
		Ocsp 응답 상태: NONE
	[출력이 생략됨]
	완료
	>
	```

6.	(선택사항) 웹 브라우저를 통해 컨텐츠에 액세스될 때 보안 경고가 발생하지 않도록 사용자는 "중간 CA" 인증서를 설치하려고 할 수 있습니다. 그러면 Citrix Netscaler VPX에서 클라이언트가 연결된 상태에서 정보를 공유할 수 있습니다.

	RapidSSL을 위한 중간 인증서를 얻으려면 다음 링크에 방문하십시오.

	* [Reissue GeoTrust Certificate For Partner Orders or QuickSSL ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://knowledge.digicert.com/solution/SO5989.html){:new_window}
  * [RapidSSL Intermediate and Root CA Certificates ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://knowledge.digicert.com/generalinformation/INFO1548.html#links){:new_window}

	인증서를 설치하고 연결하려면 이 [Citrix 기사 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://support.citrix.com/article/CTX114146){:new_window}에 있는 지시사항을 따르십시오.

	```
	> show ssl certlink
	1) 인증서 이름: hsmclient7ns  CA 인증서 이름: ICARSSL
	완료
	```
