---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, configure, tune, tuning, ssl, offload

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

# Citrix Netscaler VPX를 사용하여 SSL 오프로드 구성 및 조정
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

이 단계별 지시사항은 Citrix Netscaler VPX에서 SSL 오프로드를 구성 및 조정하는 과정을 제공하며, 이는 HSM 링크를 통해 생성된 인증서 및 암호화 자료를 사용하여 수행됩니다.

이 단계별 지시사항에서는 VPX/HSM 쌍을 주문하고 작성하기 위해 사용자가 [Citrix Netscaler VPX를 사용하여 IBM© Hardware Security Module(HSM) 배치 및 구성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx)의 단계를 완료했다고 가정합니다.
{: note}

## 배치 정보
{: #about-the-deployment}
이 배치는 다음 컴포넌트 스펙으로 빌드되고 테스트되었습니다.

| NetScaler VPX 버전 및 빌드	| HSM 소프트웨어 버전 | HSM 펌웨어 버전 | HSM 클라이언트 버전 |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: 빌드 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## 논리 토폴로지
{: #logical-topology}

다음 다이어그램은 SSL 오프로드 유스 케이스를 위한 네트워크 트래픽 플로우를 표시합니다. 이는 Citrix VPX와 HSM 어플라이언스 간의 신뢰 링크 및 구성의 시각적 퍼스펙티브와 논리적 퍼스펙티브를 제공합니다.

<img src="images/network-flows-logical-topology.jpg" alt="그림" style="width: 700px;"/>

SSL 오프로드에 익숙하지 않은 경우 이 [Citrix 기사 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}를 검토하십시오.

## 수행할 사항
{: #what-you-ll-accomplish}

이 단계별 지시사항에서는 Citrix Netscaler VPX를 위해 SSL을 구성하는 방법에 대한 정보를 제공합니다.

태스크  |설명
------------- | -------------
[인증서 설치](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) |이전 [단계별](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) 지시사항에서 작성된 SSL 인증서를 설치합니다.
[DNS 레코드 확인 및 구성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | DNS 레코드가 가상 서버로 Citrix Netscaler VPX에서 구성되도록 공용 주소를 가리키는 FQDN에 대해 존재하는지 확인합니다.
[SSL 가상 서버 추가 및 구성](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | SSL 가상 서버를 추가하고 구성합니다.
[새 암호 스트위 작성 및 적용](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | AEAD, ECDHE 및 ECDSA를 선호하고 우선순위를 지정하는 암호화 스위트를 작성합니다.

## 추가 리소스
{: #additional-resources}
다음 추가 리소스는 IBM Hardware Security Module을 사용하여 Citrix Netscaler VPX를 최대한 활용하는 데 도움을 줍니다.

* [NetScaler 12.1 제품 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Gemalto 지원 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [IBM Cloud 지원 센터](/docs/get-support?topic=get-support-using-avatar){:new_window}
