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

# DNS 가상 서버 구성
{: #configure-the-dns-virtual-server}

DNS 가상 서버를 구성하려면 다음을 수행하십시오.

1. 트래픽 관리 > 로드 밸런싱 > 서버로 이동하십시오. 
2. 추가를 클릭하여 두 가지 IBM© Softlayer DNS 분석기인 10.0.80.11 및 10.0.80.12를 추가하십시오. 

	<img src="images/fp5.png" alt="그림" style="width: 200px;"/> <img src="images/fp5b.png" alt="그림" style="width: 200px;"/>

3. 그런 다음 트래픽 관리 > 로드 밸런싱 > 서비스 그룹으로 이동하고 추가를 선택하여 DNS 서비스 그룹을 작성하고 정의하십시오. 

	<img src="images/fp6.png" alt="그림" style="width: 400px;"/> 

4. DNS 프로토콜을 선택한 후 확인을 클릭하십시오.

	<img src="images/fp7.png" alt="그림" style="width: 300px;"/> 
	
5. 다음 화면에서 먼저 **서비스 그룹 멤버** 아래의 비어 있는 필드를 클릭하여 멤버 서버로 새 DNS 분석기를 이 DNS 서비스 그룹에 추가하십시오. 

6. 서비스 그룹 멤버 작성 패널에서 DNS 포트 53을 지정한 후 작성을 클릭하십시오. 

	<img src="images/fp8.png" alt="그림" style="width: 200px;"/> 
	
7. 닫기를 클릭한 후 완료를 클릭하십시오. 

	두 개의 IBM Softlayer DNS 분석기가 Citrix NetScaler VPX 어플라이언스에서 도달할 수 있다고 간주하는 경우 서비스 그룹은 녹색으로 표시됩니다. 

8. 이제 트래픽 관리 > 로드 밸런싱 > 가상 서버로 이동한 후 추가를 클릭하여 DNS 가상 서버를 정의하십시오.
9. 기본 설정에서 가상 서버에 이름을 지정하고 DNS 프로토콜 및 포트 53을 선택한 후 사설 서브넷에서 IP 주소를 지정하십시오. 

	<img src="images/fp9.png" alt="그림" style="width: 300px;"/> 
	
10. 다음 페이지에서 **No Load Balancing virtual Server ServiceGroup Binding**으로 레이블된 비어 있는 필드를 클릭하십시오.
11. 드롭 다운 목록에서 이전에 정의된 DNS 서비스 그룹을 선택하고 바인드를 클릭하십시오.  

	<img src="images/fp10.png" alt="그림" style="width: 300px;"/> 
	
12. 완료 다음에 표시되는 계속을 클릭하십시오. 

DNS 가상 서버 상태는 이제 녹색으로 표시되어야 합니다. 

<img src="images/fp11.png" alt="그림" style="width: 500px;"/> 
