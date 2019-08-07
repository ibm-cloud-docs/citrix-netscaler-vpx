---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: terminology, nsip, snip, vip, service, object, monitor

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.vpx_full}} 용어집
{: #citrix-netscaler-vpx-terminology}

Citrix NetScaler 플랫폼은 제품별 용어와 기본 로드 밸런서 용어 및 개념을 모두 사용합니다.

### 가상 서버(Virtual Server)
{: #virtual-server}

로드 밸런싱 용어에서 가상 서버는 IP 클라이언트가 연결하는 대상 IP 주소, 포트 및 프로토콜의 조합이며 NetScaler에서 로드 밸런싱되는 특정 애플리케이션에 대한 트래픽 요청이 전송되는 위치를 나타냅니다.

### 가상 IP(VIP, Virtual IP)
{: #virtual-ip-vip-}

VIP는 클라이언트가 요청을 전송하는 대상 IP 주소입니다. NetScaler는 VIP에서 클라이언트 연결을 종료한 후 로드 밸런싱 서비스에서 구성된 서버와의 연결을 시작합니다.  이는 공용(인터넷) 트래픽의 공인 IP 주소이거나 사설(인트라넷) 트래픽의 사설 IP 주소일 수 있습니다.

### 모니터(Monitor)
{: #monitor}

서비스를 추적하여 올바르게 작동 중임을 보장할 수 있도록 하는 요소입니다. 모니터는 프로브 및 하트비트 신호를 사용하여 서비스 상태를 추적합니다.

### 서버 오브젝트(Server Object)
{: #server-object}

일반 IP 주소를 사용하는 대신 실제 서버에 의미 있는 이름을 지정할 수 있도록 하는 가상 엔티티입니다.

### 서브넷 IP(SNIP, SubNet IP)
{: #subnet-ip-snip-}

SNIP는 NetScaler가 서버(또는 오브젝트)와 통신하려고 할 때마다 NetScaler에서 사용되는 패킷의 소스 IP 주소입니다. 또한 서버는 서브넷 IP를 사용하여 NetScaler에 응답합니다.

### 서비스(Service)
{: #service}

요청을 특정 서버로 라우트하는 데 사용되는 IP 주소, 포트 및 프로토콜의 조합입니다. 서비스가 구성된 후 나중에 가상 서버와 연관되어야 합니다.

### NSIP(NetScaler IP)
{: #netscaler-ip-nsip-}

관리 목적으로 지정된 로드 밸런서의 IP입니다.




