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

# 키 작성 및 인증서 서명 요청(CSR) 생성
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

이 하위 절에서 인증서 서명 요청(CSR)을 생성하고 이를 사용하여 인증서를 주문하고 요청하는 데 사용될 키 쌍을 작성합니다.

1.	먼저 VPX에서 오브젝트 목록을 확인하십시오. 작성 중에 이 파티션에 대해 지정된 비밀번호를 사용하십시오.

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : 	**********
	```

	이 출력은 출력이 공백이고 비어 있을 때 오브젝트가 존재하지 않는지 확인합니다.

	그런 다음 파티션 세부사항을 표시하여 HSM에서 오브젝트 수가 0인지 확인합니다.

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	파티션 이름:                       partition6
	파티션 SN:                                 534071053
	파티션 레이블:                             partition6
	파티션 소유자 잠김:                        아니오
	파티션 소유자 PIN 변경:                    아니오
	남아 있는 파티션 소유자 로그인 시도 횟수:  파티션 소유자가 잠기기 전까지 10회
	레거시 도메인이 설정됨:                    아니오
	파티션 스토리지 정보(바이트):              총계=207559, 사용됨=0, 사용 가능=207559
	파티션 오브젝트 수:                        0

	명령 결과: 0(성공)
	```

	위에 나열된 명령에서 다음 구문을 사용합니다.

	```
	partition show -p <partition_name>
	```

2.	VPX에서 인증서 관리 유틸리티(CMU)를 사용하는 경우 아래 표시된 명령을 사용하여 키 쌍을 작성하십시오. 다시 한 번 지정된 파티션 비밀번호를 사용하십시오.

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	RSA 메커니즘 유형 선택 -
	[1] PKCS [2] FIPS 186-3 주요 항목만 해당 [3] FIPS 186-3 보조 주요 항목: 1
	```

	위의 구문에서 `modulusBits` 매개변수는 RSA 키의 일부 길이를 표시하며, `publicExponent`는 키의 생성에 사용될 공개 지수 값을 정의합니다(3, 7 또는 65537로 설정되어야 함). "label" 키워드는 쉽게 참조되고 나중에 식별될 수 있도록 태그를 지정하는 데 사용됩니다. 기타 두 개/추가 매개변수에 대한 자세한 정보는 [유틸리티 참조 안내서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}를 확인하십시오.

3.	오브젝트가 작성되었는지 확인하십시오. VPX에서는 다음과 같습니다.

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	HSM에서는 다음과 같습니다.

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	파티션 이름:                       partition6
	파티션 SN:                                 534071053
	파티션 레이블:                             partition6
	파티션 소유자 잠김:                        아니오
	파티션 소유자 PIN 변경:                    아니오
	남아 있는 파티션 소유자 로그인 시도 횟수:  10회. 이후에는 파티션 소유자가 잠깁니다.
	레거시 도메인이 설정됨:                    아니오
	파티션 스토리지 정보(바이트):              총계=207559, 사용됨=1660, 사용 가능=205899
	파티션 오브젝트 수:                        2

	명령 결과: 0(성공)
	```

4.	이전 단계에서 작성된 키를 사용하는 경우 CMU 유틸리티를 사용하여 CSR을 생성하십시오.

	공통 이름(CN) 및 이메일(E)에 올바른/적합한 값을 사용해야 합니다. 공통 이름(CN)은 가상 서버/IP(VPX)와 연관된 DNS A 레코드에 사용되는 FQDN과 일치해야 합니다. E 매개변수는 인증서가 요청되고/주문된 후 인증서 조달 세부사항을 전송하는 데 사용됩니다.

	```
	root@IBMADC690867-s6dr# cmu requestcertificate

	슬롯 0의 토큰에 올바른 비밀번호 입력: **********

	2자의 국가 코드(C) 제목 입력: US
	주 이름(S) 제목 입력: North Carolina
	지역 이름(L) 제목 입력: Durham
	조직 이름(O) 제목 입력: IBM
	조직 단위 이름(OU) 제목 입력: HSM
	공통 이름(CN) 제목 입력: hsmclient7.projectgoldfinch.net   
	이메일 주소(E) 입력: user@yourdomain.com
	출력 파일 이름 입력: certreqnss6dr.csr
	```

	위에 나열된 출력에서 파일 이름은 .csr 확장자를 사용하면 어떠한 이름도 사용 가능합니다. 그러나 의미 있는 설명이 포함되는 것이 좋습니다.

5.	파일의 작성을 확인하십시오.

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
