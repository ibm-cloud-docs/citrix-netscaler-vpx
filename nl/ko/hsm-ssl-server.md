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

# SSL 가상 서버 추가 및 구성
{: #add-and-configure-the-ssl-virtual-server}

SSL 가상 서버를 추가하고 구성하려면 다음 프로시저를 수행하십시오.

1. **시스템 > 설정 > 기본 기능 구성**으로 이동하십시오. **SSL 오프로딩**을 선택한 후 **확인**을 클릭하십시오.
2. NetScaler GUI에서 **트래픽 관리 > 로드 밸런싱 > 서비스 > 추가**로 이동하고 이름, IP 주소를 지정한 후 **HTTP**로 프로토콜을 설정하십시오. 완료하려면 **확인**을 누르십시오.
3. 서비스가 작동 가능한지 확인하십시오.

	<img src="images/15-confirm-service.png" alt="그림" style="width: 700px;"/>

4. 추가 서버를 위해 2단계를 반복하십시오.
5. **트래픽 관리 > 로드 밸런싱 > 가상 서버>**로 이동하여 **추가**를 클릭하십시오. 이름을 지정하고 프로토콜로 **SSL**을 선택한 후 공인 IP를 입력하십시오. 완료하려면 **확인**을 누르십시오.
6. 이제 **No Load Balancing Virtual Server Service Binding**을 선택하고 **Select**를 클릭하십시오. 이전 단계에서 작성한 서비스를 선택하고 선택을 클릭한 후 **바인드/계속**을 클릭하십시오.

	<img src="images/18-bind-service.png" alt="그림" style="width: 700px;"/>

7. 마지막으로 **서버 인증서 아님**을 클릭한 후 **서버 인증서 선택**을 클릭하고 이전에 설치한 인증서를 선택하십시오. 완료하려면 **선택**, **바인드/계속**, **완료**를 차례로 클릭하십시오.
