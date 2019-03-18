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

# 새 암호 스위트 작성 및 적용
{: #create-and-apply-a-new-cipher-suite}

암호 스위트는 SSL 및 TLS 프로토콜의 보안 설정을 조정하는 데 사용된 인증, 암호화, MAC(Message Authentication Code) 및 키 교환 알고리즘의 조합입니다.

적절한 인증을 보장하려면 Citrix Netscaler VPX에서 최적의 암호 조합을 사용하는지 확인해야 합니다.

SSL 암호 스위트 및 기타 우수 사례에 대해 알아보려면 다음 링크를 방문하십시오.

* [Citrix NetScaler를 사용하여 SSLlabs.com에서 A+ 스코어링 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.citrix.com/blogs/2018/05/16/scoring-an-a-at-ssllabs-com-with-citrix-netscaler-q2-2018-update/){:new_window} – 2018년 2분기 업데이트(명령 안내서의 3 - 5단계 참조)
* [SSL 및 TLS 배치 우수 사례 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices#23-use-secure-cipher-suites){:new_window}
* [NetScaler에서 ECC를 설정하는 방법 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://support.citrix.com/article/CTX205289){:new_window}

**참고:** 이 절에서는 SSL 암호에 필요한 구성 및 특정 구성에 대해 중점적으로 설명합니다. 이전 링크의 정보에는 SSL 오퍼레이션을 최적화하는 데 적용될 수 있는 추가 설정을 제공할 수 있습니다.

AEAD, ECDHE 및 ECDSA 암호의 우선순위를 지정하는 새 암호 스위트를 작성하려면 다음 프로시저를 수행하십시오.

1.	Citrix VPX CLI에서 다음 명령을 동시에 입력하고 모두 적용되는지 확인하십시오.

	```
	add ssl cipher SSLLABS
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-256-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-256-CBC-SHA
	```

	이전 명령의 구문은 다음과 같습니다.

	```
	add ssl cipher <cipherGroupName>
	bind ssl cipher <cipherGroupName> -cipherName <string>
	```

2.	암호가 Citrix Netscaler VPX에 추가되었는지 확인하십시오.

	```
	> show ssl cipher SSLLABS
	1)      암호 이름: TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256       우선순위: 1
	        설명: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02b
	2)      암호 이름: TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384       우선순위: 2
	        설명: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc02c
	3)      암호 이름: TLS1.2-ECDHE-ECDSA-AES128-SHA256   우선순위: 3
	        설명: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA-256   HexCode=0xc023
	4)      암호 이름: TLS1.2-ECDHE-ECDSA-AES256-SHA384   우선순위: 4
	        설명: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA-384   HexCode=0xc024
	5)      암호 이름: TLS1-ECDHE-ECDSA-AES128-SHA        우선순위: 5
	        설명: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA1   HexCode=0xc009
	6)      암호 이름: TLS1-ECDHE-ECDSA-AES256-SHA        우선순위: 6
	        설명: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA1   HexCode=0xc00a
	7)      암호 이름: TLS1.2-ECDHE-RSA-AES128-GCM-SHA256 우선순위: 7
	        설명: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02f
	8)      암호 이름: TLS1.2-ECDHE-RSA-AES256-GCM-SHA384 우선순위: 8
	        설명: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc030
	9)      암호 이름: TLS1.2-ECDHE-RSA-AES-128-SHA256    우선순위: 9
	        설명: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA-256   HexCode=0xc027
	10)     암호 이름: TLS1.2-ECDHE-RSA-AES-256-SHA384    우선순위: 10
	        설명: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA-384   HexCode=0xc028
	11)     암호 이름: TLS1-ECDHE-RSA-AES128-SHA  우선순위: 11
	        설명: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0xc013
	12)     암호 이름: TLS1-ECDHE-RSA-AES256-SHA  우선순위: 12
	        설명: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0xc014
	13)     암호 이름: TLS1.2-DHE-RSA-AES128-GCM-SHA256   우선순위: 13
	        설명: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0x009e
	14)     암호 이름: TLS1.2-DHE-RSA-AES256-GCM-SHA384   우선순위: 14
	        설명: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0x009f
	15)     암호 이름: TLS1-DHE-RSA-AES-128-CBC-SHA       우선순위: 15
	        설명: SSLv3 Kx=DH       Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x0033
	16)     암호 이름: TLS1-DHE-RSA-AES-256-CBC-SHA       우선순위: 16
	        설명: SSLv3 Kx=DH       Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0039
	17)     암호 이름: TLS1-AES-128-CBC-SHA       우선순위: 17
	        설명: SSLv3 Kx=RSA      Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x002f
	18)     암호 이름: TLS1-AES-256-CBC-SHA       우선순위: 18
	        설명: SSLv3 Kx=RSA      Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0035
 	완료
 	```

3.	가상 서버에서 기본 암호 스위트를 바인드 해제하고 이전 단계에서 작성된 사용자 정의 그룹을 바인드하십시오.

	```
	unbind ssl vserver https_vip2 -cipherName DEFAULT

	bind ssl vserver https_vip2 -cipherName SSLLABS

	bind ssl vserver https_vip2 -eccCurveName ALL
	```

	이전 명령의 구문은 다음과 같습니다.

	```
	unbind ssl cipher <cipherGroupName> -cipherName <string>
	bind ssl vserver <vServerName> -cipherName <string>
	bind ssl vserver <vServerName> -eccCurveName <eccCurveName>
	```

4.	가상 서버의 변경사항을 확인하십시오.

	```
	> show ssl vserver https_vip2

	[출력이 생략됨]
		ECC 곡선: P_256, P_384, P_224, P_521

	1)      CertKey 이름: hsmclient7ns      Server Certificate

	1)      암호 이름: SSLLABS
		설명: 사용자가 암호 그룹을 작성함
 	완료
	```

5.	(선택사항) HTTP 경로 재지정을 통해 HTTP 요청 작성 시(HTTPS와 반대로) 사용자를 보안 웹 사이트로 경로 재지정할 수 있습니다.

	구성 지시사항은 [How to Configure HTTP to HTTPS Redirection on NetScaler ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.citrix.com/article/CTX201201){:new_window}의 내용을 참조하십시오.

6.	웹 브라우저를 열고 FQDN을 입력하여 HTTPS 연결을 테스트하십시오. 사이트는 Citrix VPX 뒤의 HTTP 서비스로 렌더링된 컨텐츠를 로드해야 합니다.

	인증서 정보를 표시하기 위해 브라우저의 URL 옆에 있는 패드락 아이콘을 클릭하여 인증서 세부사항을 볼 수도 있습니다.

	<img src="images/21-check-certificate.png" alt="그림" style="width: 350px;"/>

	5단계에서 경로 재지정이 구성된 경우 HTTP 요청 사용 시 보안 사이트도 로드됩니다.
