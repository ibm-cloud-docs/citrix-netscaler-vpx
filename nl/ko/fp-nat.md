---



copyright:
  years: 2017
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 아웃바운드 트래픽을 위한 소스 NAT 구성
{: #configure-source-nat-for-outbound-traffic}

네트워크 주소 변환(NAT)은 패킷이 트래픽 라우팅 디바이스에서 전송 중인 동안 패킷의 IP 헤더에 있는 네트워크 주소 정보를 수정하여 하나의 IP 주소 공간을 다른 IP 주소 공간으로 다시 맵핑하는 방법입니다.

Citrix NetScaler VPX 어플라이언스를 활용하여 클라이언트 머신의 아웃바운드 트래픽에서 NAT를 수행할 수 있습니다. 이를 위해 다음을 수행하십시오.

1. 시스템 > 네트워크 > 라우트로 이동하고 **RNAT** 탭으로 이동하십시오. **RNAT 구성**을 클릭하십시오.

2. RNAT를 적용할 소스 서브넷(및 마스크)을 지정하고 **확인**을 클릭하십시오.

이 서브넷의 IP에서 제공된 인터넷 연결 트래픽이 이제 Citrix NetScaler의 공인 IP 주소에서 tradfic에 대한 NAT를 사용합니다.    
