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

# Citrix Netscaler VPX를 사용하여 IBM Hardware Security Module(HSM) 배치 및 구성
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

이 단계별 지시사항은 Citrix Netscaler VPX를 사용하여 HSM을 통합하는 과정을 제공합니다. 그런 다음 두 서비스는 인증서를 작성하는 데 필요한 암호화 자료를 전달하고 생성할 수 있습니다.

## 배치 정보
이 배치는 다음 컴포넌트 스펙으로 빌드되고 테스트되었습니다.

| NetScaler VPX 버전 및 빌드	| HSM 소프트웨어 버전 | HSM 펌웨어 버전 | HSM 클라이언트 버전 |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: 빌드 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

**참고:** VPX의 이전 버전이 있거나 IBM© Cloud 플랫폼을 통해서만 디바이스를 주문할 때 선택사항 옵션으로 11.1 이전 버전만 참조하는 경우 이 안내서에 설명된 설정을 완료할 수 있도록 디바이스를 업그레이드할 수 있습니다.  

## 논리 토폴로지
다음 다이어그램은 SSL 오프로드 유스 케이스를 위한 네트워크 트래픽 플로우를 표시합니다. 이는 VPX와 HSM 어플라이언스 간의 신뢰 링크 및 구성의 시각적 퍼스펙티브와 논리적 퍼스펙티브를 제공합니다. 

<img src="images/network-flows-logical-topology.jpg" alt="그림" style="width: 700px;"/>

SSL 오프로드에 익숙하지 않은 경우 이 [Citrix 기사](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html)를 검토하십시오.

## 수행할 사항

이 단계별 지시사항에서는 Citrix Netscaler VPX를 사용하여 HSM을 배치 및 구성하는 방법에 대한 정보를 제공합니다.

태스크  |설명
------------- | -------------
[HSM(Hardware Security Module) 주문](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) | 먼저 HSM을 주문해야 합니다.
[Citrix Netscaler VPX 주문](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) |아직 Citrix Netscaler VPX가 없으면 주문해야 합니다.
[HSM 초기화](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) |대부분의 구성에는 HSM 디바이스의 초기화가 필요합니다. 그렇지 않으면 특정 `show` 명령만 실행될 수 있습니다. 
[파티션 작성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition) |파티션은 HSM 엔진에서 암호화 오브젝트를 요청하거나 작성하는 클라이언트에 연관되거나 연결되는 논리적이고 독립적인 공간입니다.
[HSM 클라이언트 소프트웨어 설치](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software) |이 하위 절에서 HSM과 상호 작용하는 데 필요한 소프트웨어 및 유틸리티와 함께 VPX가 설치됩니다. |
[NTL(Network Trust Link) 설정](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) |NTL(Network Trust Link)은 통신할 HSM(Hardware Security Module) 및 클라이언트를 위한 보안 채널입니다. |
[키 작성 및 인증서 서명 요청(CSR) 생성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) |이 하위 절에서 인증서 서명 요청(CSR)을 생성하고 이를 사용하여 인증서를 주문하고 요청하는 데 사용될 키 쌍을 작성합니다. | 
[인증서 주문](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) | Citrix Netscaler VPX를 위한 SSL 인증서를 주문합니다.
[인증서 검색 및 전송](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) | 이전에 주문한 SSL 인증서를 검색하고 다음 단계별 지시사항의 설치 및 구성을 위해 모든 사항을 준비합니다. 
