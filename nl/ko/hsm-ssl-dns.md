---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, dns, security, check, configure

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

# DNS 레코드 확인 및 구성
{: #check-and-configure-the-dns-record}

단계별 예제에서 IBM© Cloud Internet Services의 DNS 서비스는 DNS 구역 및 해당 레코드를 관리하는 데 사용됩니다. 해당 경우 레코드가 사용 중인 FQDN에 대해 작성되는지 확인해야 합니다. 레코드는 {{site.data.keyword.vpx_full}} 가상 서버에 구성되도록 공용 주소를 가리켜야 합니다.

<img src="images/12-add-record.png" alt="그림" style="width: 700px;"/>

Citrix VPX에 사용될 정적 공인 IP는 **디바이스 > 디바이스 목록**으로 이동한 후 {{site.data.keyword.vpx_full}}의 이름을 선택하여 고객 포털에서 검색될 수 있습니다.

<img src="images/13-check-ip.png" alt="그림" style="width: 300px;"/>
