---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"

keywords: setup, proxy, forward, vip, subnet

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 전달 프록시로 Citrix Netscaler VPX 설정
{: #setting-up-citrix-netscaler-vpx-as-a-forwarding-proxy}

전달 프록시는 내부 네트워크의 클라이언트와 인터넷 간의 단일 제어 지점 역할을 합니다. 프록시를 사용하면 네트워크 또는 보안 관리자가 인터넷 사이트에 대한 액세스를 제한하는 정책을 작성할 수 있습니다.

내부 네트워크의 클라이언트가 요청을 시작하면 프록시의 IP 주소가 인터넷의 원격 서버에 대한 요청을 시작하는 데 사용됩니다. 이어서 원격 서버가 프록시에 다시 응답하고 프록시가 클라이언트에 응답을 리턴합니다.

일반적으로 프록시는 방화벽과 결합되어 내부 네트워크에 있는 클라이언트의 보안을 보장합니다.

## 1단계: 사설 네트워크에서 사용할 VIP 요청
{: #step-1-request-vips-to-use-in-the-private-network}

{{site.data.keyword.BluSoftlayer_notm}} 고객 포털에서 Citrix NetScaler VPX 로드 밸런서를 주문하면 역방향 프록시를 요청하는 것으로 간주됩니다. 요청자에게 가상 IP(VIP)로 사용될 "공인" IP의 수를 묻습니다.

전달 프록시의 경우 사설 네트워크에서 VIP를 설정해야 합니다. 사설 네트워크용 VIP를 요청하려면 지원 티켓을 열어야 합니다. 필요한 VIP의 수에 따라 티켓에서 요청되는 서브넷의 크기가 결정됩니다. 서브넷 정보가 티켓에 리턴됩니다.

이 예에서는 `/29` 서브넷을 요청했으며 다음과 같은 결과가 나타납니다.

* 사설 VIP로 사용하도록 작성된 서브넷 `10.114.27.0/29`

* 서브넷 IP(SNIP) `10.114.52.101` 및 라우팅된 서브넷 `10.114.27.0/29`

* 지원 팀에서 VIP `10.114.27.0-3`을 Citrix NetScaler VPX에 추가함

## 2단계: Citrix NetScaler VPX에서 로드 밸런싱 및 캐시 경로 재지정 기능 사용
{: #step-2-enable-load-balancing-and-cache-redirect-features-on-the-citrix-netscaler-vpx}

기본적으로 Citrix NetScaler VPX 로드 밸런서의 로드 밸런싱 및 캐시 경로 재지정 기능이 사용 안함으로 설정됩니다. `enable ns feature cr lb` 명령을 통해 이러한 기능을 사용으로 설정합니다.


## 3단계: 전달 프록시 작성
{: #step-3-create-the-forward-proxy}

명령행을 사용하여 Citrix NetScaler VPX에서 다음 명령을 실행하십시오. 이 시나리오에서는 두 개의 {{site.data.keyword.BluSoftlayer_notm}} DNS 서버 중 하나만 추가됩니다.  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

1행은 경로 재지정 캐시를 작성합니다. 프로토콜은 HTTP이며 `10.114.27.3`는 사설 네트워크에서 요청된 VIP 중 하나입니다. 포트는 HTTP용 기본 포트 80이지만 이 주소 및 포트 조합이 브라우저에서 프록시 명령문으로 사용되므로 포트를 필요한 값으로 변경할 수 있습니다.

2행은 "실제" DNS를 나타내는 로드 밸런싱 VIP를 추가합니다.

3행은 "실제" DNS의 IP 주소를 서비스로 추가합니다. 이 주소는 고객 DNS이거나 {{site.data.keyword.BluSoftlayer_notm}} 제공 DNS 분석기로 다시 라우팅될 수 있습니다.

4행은 VIP를 "실제" 서버에 바인드합니다. `10.114.27.4`에 대한 모든 DNS 요청이 `10.0.80.12`로 전송됩니다.

5행은 이름 분석을 위해 가상 DNS를 사용하도록 전달 프록시 가상 서버에 알립니다.

## 클라이언트 구성
{: #configuring-the-client}

전달 프록시를 사용하도록 클라이언트 사용자 정의를 계속하기 전에 클라이언트에서 Firefox 브라우저를 사용하여 공용 사이트(예: http://www.ibm.com) 에 연결할 수 없는지 확인하십시오. 클라이언트에는 공용 인터페이스가 없어야 하므로 이 요청이 실패해야 합니다.

다음 예에서는 Linux 클라이언트를 구성합니다.

클라이언트에 몇 가지 변경사항을 작성해야 합니다. 첫 번째 변경사항은 클라이언트의 분석기가 가상 DNS를 가리키도록 하는 것이며, 이는 두 가지 방법 중 하나로 수행할 수 있습니다.

DNS의 가상 주소를 가리키도록 수동으로 `/etc/resolv.conf`를 편집할 수 있습니다. 클라이언트 관리 도구를 사용하여 이러한 변경사항을 원래 설정으로 되돌릴 수 있습니다.  

또는 `/etc/sysconfig/network-scripts/ifcfg-ethx` 인터페이스를 편집하여 `DNS1=` 명령문을 추가할 수 있습니다. 설정된 후 서비스 네트워크 다시 시작 명령을 실행하여 변경사항을 적용할 수 있습니다.

두 경우 모두 DNS IP 주소를 가상 DNS 주소로 구성해야 하며 요청이 Citrix NetScaler VPX 전달 프록시를 가리키도록 클라이언트의 브라우저를 구성해야 합니다.

Firefox 내에서 다음 단계를 사용하여 필요한 변경사항을 작성하십시오.

1. **환경 설정 > 고급 > 네트워크 > 연결 설정**을 클릭하십시오.

* **수동 프록시 구성**을 선택하고 다음을 입력하십시오.

  * **주소:** 10.114.27.3

  * **포트:** 80

  * **모든 프로토콜에 이 프록시 서버 사용** 선택란을 선택하십시오.

* **저장**을 클릭하고 브라우저 창을 닫으십시오.

IP 주소 `10.114.27.3`은 1단계에서 작성된 전달 캐시의 IP 주소입니다.

이 시점에서 설정이 완료되며 사설 네트워크의 격리된 리소스에서 인터넷에 액세스할 수 있습니다.

## 설정 유효성 검증
{: #validating-the-setup}

클라이언트가 전달 프록시를 사용하도록 구성되었으므로 공용 사이트에 다시 액세스해 보십시오. 이제 요청이 성공해야 합니다.

다음 표시 명령을 사용하여 전달 프록시 상태의 유효성을 검증할 수 있습니다.

**show cr policy:** 기존 캐시 경로 재지정 정책을 모두 표시합니다.

**show policy map:** 구성된 맵 정책 및 관련 맵 정책 정보를 표시합니다.

**show cr vserver:** 지정된 캐시 경로 재지정 가상 서버 또는 구성된 모든 캐시 경로 재지정 가상 서버를 표시합니다.

**stat cr vserver:** 캐시 경로 재지정 Vserver 통계를 표시합니다.

Citrix의 기본 전달 프록시 구성은 매우 간단합니다. 내부 네트워크의 클라이언트에게 인터넷의 리소스에 대한 보안 경로를 부여하는 방법을 제공합니다. 또한 네트워크 관리자가 네트워크에 대한 제어 레벨을 유지할 수 있도록 합니다.

고객 사이트에서 구현하는 경우 구성에 방화벽을 추가하여 리소스 보호를 강화하는 것이 좋습니다.
