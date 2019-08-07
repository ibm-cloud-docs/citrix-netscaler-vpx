---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: security, hsm, ntl, certificate

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

# NTL(Network Trust Link) 설정
{: #establish-a-network-trust-link-ntl-}

NTL(Network Trust Link)은 통신할 HSM(Hardware Security Module) 및 클라이언트를 위한 보안 채널입니다. NTL은 HSM 서버 파티션 및 클라이언트 간에 전송된 데이터를 인증하고 암호화하기 위해 양방향에서 인증서를 사용합니다.

신뢰 링크에는 모든 프로세스 및 유틸리티가 올바르게 작동할 수 있도록 NTLS 및 NTLA(양방향) 프로토콜 모두에서 TCP 포트 1792에 액세스할 수 있어야 합니다.

NTL을 설정하려면 다음 프로시저를 수행하십시오.

1.	`/var/safenet/safenet/lunaclient/bin` 디렉토리로 이동하고 VTL 유틸리티를 사용하여 인증서를 작성하십시오.

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	개인 키가 작성되고 쓰기가 수행된 위치: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	인증서가 작성되고 쓰기가 수행된 위치: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**참고:** 클라이언트 인증서에 사용된 ID는 클라이언트 인증서에 지정된 사설 IP입니다. 이를 통해 나중에 HSM에서 사용되고 참조됩니다.

2. SCP를 사용하여 인증서 파일을 HSM 서버로 전송하십시오.

	```
	root@IBMADC690867-s6dr# scp /var/safenet/safenet/lunaclient/cert/client/	10.121.229.224.pem hsm_admin@10.121.229.201:

	호스트의 인증 '10.121.229.201 (10.121.229.201)'을 설정할 수 없습니다.

	ECDSA 키 지문은 SHA256:UBltOfaDojRlUVxDXh6zI3CPMF8FRaJnls0uxeWgrCY입니다.

	연결을 계속하시겠습니까(예/아니오)? 예

	경고: 알려진 호스트의 목록에 '10.121.229.201'(ECDSA)이 영구적으로 추가되었습니다.

	hsm_admin@10.121.229.201의 비밀번호:

	10.121.229.224.pem                                                 
	100%  818     	
	1.6MB/s   
	00:00
	```

	VTL(Virtual Token Library)에 대해 자세히 알아보려면 [유틸리티 참조 안내서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}를 참조하십시오.

3.	SCP를 사용하여 HSM 서버 인증서 파일을 {{site.data.keyword.vpx_full}} 클라이언트에 전송한 후 서버를 추가하십시오.

	```
	root@IBMADC690867-s6dr# scp hsm_admin@10.121.229.201:server.pem .
	hsm_admin@10.121.229.201의 비밀번호:

	server.pem                                                         
	100% 1180     	
	2.3MB/s   
	00:00

	root@IBMADC690867-s6dr# vtl addServer -n 10.121.229.201 -c server.pem

	새 서버 10.121.229.201이 서버 목록에 추가되었습니다.
	```

	위에 사용된 구문은 다음과 같습니다.

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. 서버의 추가 항목을 확인하십시오.

	```
	root@IBMADC690867-s6dr# vtl listservers
	서버: 10.121.229.201  HTL 필요: 아니오
	```

4.	HSM에서 기존 클라이언트를 보려면 다음 명령을 실행하십시오.

	```
	[jpmongehsm2] lunash:>client list

	등록된 클라이언트 1: NS-IBMADC690867-d85b
	등록된 클라이언트 2: NS-IBMADC690867-4v36
	등록된 클라이언트 3: NS-jpmongevsi05win2012vsi-4v36
	등록된 클라이언트 4: NS-IBMADC690867-k8ru
	등록된 클라이언트 5: NS-IBMADC690867-wnzs

	명령 결과: 0(성공)
	```

5.	새 클라이언트로 VPX를 등록하십시오.

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	'client register'에 성공했습니다.

	명령 결과: 0(성공)
	```

	이전 명령에서 다음 구문을 사용합니다.

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	클라이언트 이름은 IBM© Cloud에 지정되고 사용된 ID와 일치할 필요가 없습니다. 그러나 이름이 계속해서 일치하는 것이 좋습니다.

6. 클라이언트가 추가되었는지 확인하십시오.

	```
	[jpmongehsm2] lunash:>client list

	등록된 클라이언트 1: NS-IBMADC690867-d85b
	등록된 클라이언트 2: NS-IBMADC690867-4v36
	등록된 클라이언트 3: NS-jpmongevsi05win2012vsi-4v36
	등록된 클라이언트 4: NS-IBMADC690867-k8ru
	등록된 클라이언트 5: NS-IBMADC690867-wnzs
	등록된 클라이언트 6: NS-IBMADC690867-s6dr

	명령 결과: 0(성공)
	```

7. 파티션을 클라이언트에 지정하십시오. 이전에 작성된 파티션을 참조해야 합니다. 이름이 이전 단계에 표시된 클라이언트의 ID와 일치하는지도 확인해야 합니다.

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition'에 성공했습니다.

	명령 결과: 0(성공)
	```

	이전 출력에서 다음 구문을 사용합니다.

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	Citrus Netscaler VPX에서 연결을 확인하십시오.

	```
	root@IBMADC690867-s6dr# vtl verify

	다음 Luna SA 슬롯/파티션이 발견되었습니다.

	슬롯         일련 번호               레이블
	====    ================        =====
	0           534071053        partition6
	```

	`vtl verify`에 표시된 출력은 파티션의 "슬롯 번호", 일련 번호 및 이 신뢰 링크에 바인드된 파티션의 이름을 나열합니다. 기타 출력에는 문제가 표시됩니다.

	또한 `/etc` 디렉토리에 위치한 Chrystoki 파일에 있는 인증서 및 서버의 경로를 확인하는 것도 좋습니다. 이를 위해 다음을 수행하십시오.

	```
	root@IBMADC690867-s6dr# cd /etc/
	root@IBMADC690867-s6dr# cat /etc/Chrystoki.conf
	Chrystoki2 = {
		LibUNIX64 = /var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so;
		}

	[출력이 생략됨]
		ClientPrivKeyFile = /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem;
		ClientCertFile = /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem;
		ServerCAFile = /var/safenet/safenet/lunaclient/cert/server/CAFile.pem;
		NetClient = 1;
		HtlDir = /var/safenet/safenet/lunaclient/htl/;
		ServerName00 = 10.121.229.201;
		ServerPort00 = 1792;
		ServerHtl00 = 0;
	}
	[출력이 생략됨]
	```

9.	구성을 저장하십시오.

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	여기에 사용된 복사 명령은 VPX의 다시 부팅에서 구성 지속성을 수행합니다.

10.	암호화 오퍼레이션에 필요한 safenet 게이트웨이 클라이언트 프로세스를 시작하십시오.

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. 프로세스가 실행 중인지 확인하십시오.

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. 마지막으로 이 프로세스가 다시 부팅 프로세스 중에 자동으로 시작되었는지 확인하십시오.

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

이제 NTL(Network Trust Link)이 설정되었습니다.
