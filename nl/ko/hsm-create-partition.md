---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: partition, create, security, hsm

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

# 파티션 작성
{: #create-a-partition}

파티션은 HSM 엔진에서 암호화 오브젝트를 요청하거나 작성하는 클라이언트에 연관되거나 연결되는 논리적이고 독립적인 공간입니다. 각 파티션에는 다른 파티션과 격리된 고유한 데이터 및 정책이 있습니다. 파티션에 대해 알아보려면 [관리 안내서(211페이지) ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}를 참조하십시오.

파티션을 작성하려면 다음 프로시저를 수행하십시오.

1.	[초기화](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) 중에 지정된 비밀번호를 사용하여 HSM 보안 담당자/관리자로 로그인하십시오.

	```
	[jpmongehsm2] lunash:>hsm login

	HSM 관리자의 비밀번호를 입력하십시오.
	> ********

	'hsm login'에 성공했습니다.

	명령 결과: 0(성공)
	```

2.	HSM 관리자 로그인 상태가 "로그인되어 있음"인지 확인하십시오.

	```
	[jpmongehsm2] lunash:>hsm show

	어플라이언스 세부사항:
	==================
	소프트웨어 버전:                6.2.2-5

	HSM 세부사항:
	============
	HSM 레이블:                         jpmonge
	일련 번호:                          534071
	펌웨어:                             6.10.9
	HSM 모델:                           K6 Base
	인증 방법:                          비밀번호
	HSM 관리자 로그인 상태:             로그인되어 있음
	남아 있는 HSM 관리자 로그인 횟수:   3회. 이후에는 HSM이 무효화됩니다!
	RPV 초기화:                         아니오
	감사 역할 초기화:                   아니오
	원격 로그인 초기화:                 아니오
	수동으로 무효화:                    아니오
	[출력이 생략됨]
	```

	위의 출력은 HSM 관리자 로그인 상태에서 `Logged In`을 표시해야 합니다. 그렇지 않으면 위의 절에 나열된 대부분의 오퍼레이션 및 명령은 관리자 액세스가 필요할 때 실패하게 됩니다.

3.	기존 파티션 나열:

	```
	[jpmongehsm2] lunash:>partition list
	스토리지(바이트)
	----------------------------
	파티션               이름                   오브젝트 총계       사용됨 사용 가능
	===================================
	534071016            partition1                   0  207559       0  207559 	534071020            partition2                   3  207559    3464  204095
	534071027            partition3                   0  207559       0  207559
	534071021            partition4                   2  207559    1652  205907
	534071030            partition5                  10  207559    9400  198159

	명령 결과: 0(성공)
	```

	이 출력은 다섯 개의 기존 파티션을 표시합니다.

4.	새 파티션 작성:

	 이 단계에서 정의된 비밀번호는 나중에 Citrix VPX HSM 클라이언트 프로세스에서 오브젝트를 연관시키고 작성하는 데 사용됩니다. 나중에 참조하기 위해 이 비밀번호를 추적하십시오. 또한 초기화 프로세스 중에 정의된 복제 도메인을 사용해야 합니다.
   {: note}

	```
	[jpmongehsm2] lunash:>partition create -partition partition6

	완료 시 여섯 개의 파티션이 제공됩니다.

	-label: 제공되지 않으며, 레이블에 이름을 사용합니다.

	이 파티션의 비밀번호를 입력하십시오.
	> **********

	확인을 위해 비밀번호를 다시 입력하십시오.
	> **********

	이 파티션 작성 시 사용할 복제 도메인을 입력하십시오.
	> ********

	확인을 위해 복제 도메인을 다시 입력하십시오.
	> ********

	초기화된 파티션을 작성하려면 'proceed'를 입력하고, 지금 중지하려면 'quit'를 입력하십시오.
		> proceed
	'partition create'에 성공했습니다.

	명령 결과: 0(성공)
	```

	구문 위치:

	```
	partition create -partition <name-for-new-Partition>
	```

5.	새 파티션이 작성되었는지 확인하십시오.

	```
	[jpmongehsm2] lunash:>partition list

	스토리지(바이트)	                                             	----------------------------
	피티션               이름                   오브젝트 총계     사용됨 사용 가능
	===========================================
	534071016            partition1                   0  207559       0  207559
	534071020            partition2                   3  207559    3464  204095
	534071027            partition3                   0  207559       0  207559
	534071021            partition4                   2  207559    1652  205907
	534071030            partition5                  10  207559    9400  198159
	534071053            partition6                   0  207559       0  207559

	명령 결과: 0(성공)
	```

	`Partition List` 명령의 출력에서 이제 여섯 개의 파티션이 표시됩니다.
