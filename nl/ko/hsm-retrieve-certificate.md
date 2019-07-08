---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, retrieve, transfer, certificate

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

# 인증서 검색 및 전송
{: #retrieve-and-transfer-the-certificate}

다음 단계별 지시사항인 [Citrix Netscaler VPX를 사용하여 SSL 오프로드 구성 및 조정](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx)에서 설치하고 구성할 준비가 되도록 이전에 주문한 SSL 인증서를 검색하십시오.

1. 도메인의 소유권을 유효성 검증한 직후 인증서 이행 완료와 인증서 자체를 확인하는 이메일을 수신해야 합니다.

	`---BEGIN CERTIFICATE---`에서 `---END CERTIFICATE---`까지 텍스트를 복사하고 `.cer` 확장자를 사용한 새 인증서 파일로 컨텐츠를 저장하십시오.

2. Citrix Netscaler VPX에서 인증서 파일을 `/nsconfig/ssl` 디렉토리에 복사하십시오.

  <img src="images/11-transfer-certificate.png" alt="그림" style="width: 600px;"/>

Citrix Netscaler VPX는 이제 SSL을 사용하여 인증서를 로드 밸런싱 배치로 통합할 준비가 되었습니다.
