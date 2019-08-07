---

copyright:
  years: 2019
lastupdated: "2019-04-08"

keywords: ipsec, vpn, vpx, tunnel

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

# {{site.data.keyword.vpx_full}}의 필수 기능 사용
{: #enable-required-features-in-vpx}

IPSec VPN 작성을 위해 VPX의 필수 기능을 사용으로 설정할 수 있습니다. 

1.	VPX GUI(그래픽 사용자 인터페이스)에 액세스하십시오. 
2.	**시스템 > 설정 > 모드 구성**으로 이동하여 **계층 3 모드(IP 전달)**를 사용으로 설정하십시오. 
3.	**시스템 > 설정 > 고급 기능 구성**으로 이동하여 **클라우드 브릿지**를 사용으로 설정하십시오.

CLI에서 이러한 기능을 사용으로 설정하려면 다음 명령을 실행하십시오. 

```
> enable ns feature CloudBridge
> enable ns mode L3

```

GUI 또는 SSH를 사용한 NetScaler 연결에 대한 추가 지시사항을 보려면 [다음 기사](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler)를 방문하십시오.
