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

# IBM Hardware Security Module(HSM) 초기화
{: #initialize-ibm-hardware-security-module-hsm-}

대부분의 구성에는 HSM 디바이스의 초기화가 필요합니다. 그렇지 않으면 특정 `show` 명령만 실행될 수 있습니다.

디바이스를 초기화하려면 다음 단계를 수행하십시오.

1.	**디바이스 > 디바이스 목록 > HSM 이름 펼치기** 아래의 제어 포털에 나열된 인증 정보와 함께 SSH를 사용하여 IBM© Hardware Security Module 디바이스에 연결하십시오. 

	또는 공개 키 인증을 사용할 수 있습니다. 자세한 정보는 [어플라이언스 관리 안내서(38페이지) ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}를 참조하십시오.

	**참고:** 기본적으로 SSH 액세스는 사용으로 설정되고 허용됩니다. SSH와의 연결 문제가 있으면 인프라 라우팅 및 보안을 확인하십시오.

2. `hsm init` 명령을 실행하십시오.

	```
	[jpmongehsm2] lunash:>hsm init -l jpmonge

	HSM 관리자의 비밀번호를 입력하십시오.
	> **********

	확인을 위해 비밀번호를 다시 입력하십시오.
	> ********

	이 HSM을 초기화하기 위해 사용할 복제 도메인을 입력하십시오.
	> ********

	확인을 위해 복제 도메인을 다시 입력하십시오.
	> ********

	주의: 이 HSM을 초기화하시겠습니까?

	HSM을 초기화하려면 'proceed' 를 입력하고, 지금 중지하려면
		'quit'를 입력하십시오.
		> proceed
		'hsm init'에 성공했습니다.

	명령 결과: 0(성공)
  	```

	여기서, 사용되는 구문은 다음과 같습니다. `hsm init -l <hsmlabel>`

`-l` 매개변수 또는 레이블은 HSM에 ID를 지정하는 데 사용되는 매개변수이며 이를 이행하는 비즈니스, 관리자 또는 역할과 관련된 의미 있는 텍스트 또는 설명이 될 수 있습니다. HSM 관리자 비밀번호는 HSM 보안 담당자(SO)에 지정된 비밀번호이며 HSM 환경을 변경할 뿐만 아니라 암호화 오브젝트를 작성하고 구성하는 데 필요한 필수적인 프로파일입니다.

마지막으로 복제 도메인은 HSM 그룹 중에 오브젝트를 형성할 수 있는 공유된 ID입니다. 이는 일반적으로 백업 및/또는 HA에 사용됩니다.

HSM CLI에 지원되는 사용 가능한 모든 명령은 [LunaSH 명령 참조 안내서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window}를 참조하십시오.
