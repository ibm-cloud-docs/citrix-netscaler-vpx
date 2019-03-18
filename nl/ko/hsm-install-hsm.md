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

# IBM Hardware Security Module(HSM) 클라이언트 소프트웨어 설치
{: #install-the-ibm-hardware-security-module-hsm-client-software}

이 단계에서 HSM과 상호 작용하는 데 필요한 소프트웨어 및 유틸리티와 함께 Citrix VPX가 설치됩니다.

**참고:** 이 프로시저의 1단계 및 2단계는 선택사항이며 safenet 디렉토리와 이 디렉토리 내의 파일 또는 하위 폴더가 `/var` 경로에서 누락된 경우에만 필요합니다. 이 리소스는 클라이언트 소프트웨어로 설치될 VPX에 필요하며 클라이언트 소프트웨어를 통해 HSM 소프트에어와 연관된 유틸리티를 실행할 수 있습니다.

인증 정보를 찾아 **디바이스 > 디바이스 목록 > VPX 이름 펼치기** 아래의 제어 포털에 나열된 NetScaler CLI에 액세스하십시오.

<img src="images/3-VPX-Credentials.png" alt="그림" style="width: 400px;"/>

안내서의 이 절 및 나머지 부분에 필요합니다.

**참고:** 이 문서의 모든 VPX 명령 및 출력이 `netscalername#`(쉘 실행 표시) 또는 `>`(VPX CLI 자체용)에 나열됩니다.

1.	(선택사항) `safenet_dirs.tar` 파일을 얻고 이 파일을 `/var` 디렉토리의 VPX에 전송하십시오. `safenet_dirs.tar` 파일은 [여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window}에서 얻을 수 있습니다.

	**참고:** 위의 링크에 액세스하려면 SoftLayer 계정에 로그인해야 합니다.

	<img src="images/4-transfer-safenet_dirs.png" alt="그림" style="width: 600px;"/>

	이 이미지는 `safenet_dir.tar` 파일을 Citrix VPX에 전송하는 WinSCP 소프트웨어를 표시합니다.

2.	(선택사항) `tar` 파일을 추출하십시오.

	```
	root@IBMADC690867-wnzs# tar -xvpf safenet_dirs.tar
	x safenet/
	x safenet/config/
	x safenet/gateway/
	x safenet/SAClient_600.tgz
	x safenet/SAClient_622.tgz
	x safenet/install_client.sh
	x safenet/gateway/start_safenet_gw
	x safenet/gateway/gw_delay
	x safenet/config/safenet_config
	x safenet/config/Chrystoki.conf
	```

3.	`/var/safenet` 디렉토리로 이동하고 전송된 폴더 및 파일을 확인하십시오.

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	버전 622를 사용하여 설치 스크립트를 실행하십시오.

	```
	root@IBMADC690867-s6dr# install_client.sh -v 622
	*********************************************
	현재 버전: 622
	설치 버전: 622
	SAClient_622.tgz 파일 추출 시작
	SAClient_622.tgz 파일 추출
	SAClient_622.tgz 파일 제거

	*********************************************

	이제 Citrix edocs에서 온라인으로 사용 가능한 구성 단계 문서를 따르십시오.
	*********************************************
	```

5.	safenet 디렉토리의 작성을 확인하십시오.

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	`/var/safenet/config/` 디렉토리로 이동하고 `safenet_config` 스크립트를 실행하십시오.

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	`/etc/Chrystoki.conf` 및 기호 링크인 `/usr/lib/libCrystoki_64`가 작성되었는지 확인하십시오.

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

IBM© Hardware Security Module(HSM) 이 설치되었습니다.
