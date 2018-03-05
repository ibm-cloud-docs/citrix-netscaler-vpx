---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 기본 로드 밸런싱 구성
일반 사용자가 중요한 정보가 필요하지 않은 계정에 등록할 수 있는 기본 소셜 커뮤니티 웹 사이트가 있는 회사를 가정하십시오. 이후 사용자가 로그인하여 애완동물의 사진을 게시할 수 있습니다. 세 개의 웹/애플리케이션 서버와 이를 백업하기 위한 하나의 데이터베이스 서버가 있습니다. 도메인 및 DNS는 {{site.data.keyword.BluSoftlayer_notm}}로 호스팅되며 NetScaler 및 웹/앱 서버는 환경이 소규모이므로 모두 동일한 VLAN에 있습니다.이렇게 하면 NetScaler가 기본 로드 밸런싱 정책을 설정하기 위해 추가 구성이 필요하지 않으므로 작업이 간소해집니다. 다음 프로시저는 이 인스턴스의 트래픽 플로우에 대한 매우 간략한 설명입니다.

1. 사용자가 브라우저에 URL을 입력합니다.
2. URL의 DNS 레코드가 NetScaler의 공인 IP 중 하나를 가리킵니다.
3. NetScaler가 해당 VIP에서 트래픽을 수신하고 사용 중인 트래픽의 프로토콜(HTTP 포트 80 트래픽)을 기억합니다.
4. 그런 다음 NetScaler가 정의된 밸런싱 메소드(라우드 로빈, 지속성 IP 등)를 기반으로 서버 풀에 있는 서버 중 하나에 트래픽을 전달합니다.
5. 그런 다음 서버가 트래픽을 허용하고 사용자가 연결하여 로그인합니다.

이를 수행하려면 NetScaler가 이 트래픽을 처리하도록 구성되어야 합니다. VIP, DNS 서버의 IP 및 SNIP가 이미 구성되었으므로 이로 인해 구성이 간소화됩니다. 

NetScaler GUI에서 Configuration 화면의 왼쪽에 있는 **Traffic Management**를 펼치십시오. **Load Balancing**이라는 제목의 하위 섹션을 펼치십시오. 그런 다음, 이 프로시저에 따라 로드 밸런싱 정책에 포함될 대상 서버를 NetScaler에 알리십시오.

1. Load Balancing 아래에서 **Servers**를 클릭하십시오.
2. **Add**를 클릭하십시오.
3. 서버의 Server Name(예: Web1)을 입력하십시오.
4. 서버의 IP Address를 입력하십시오.
5. 이 시나리오에서는 기본 트래픽 도메인만 사용되기 때문에 **Traffic Domain** 필드를 공백으로 두십시오.
6. 이 서버에 대한 원하는 주석을 입력하십시오.
7. **Create**를 클릭하십시오.

풀에 있는 모든 서버에 대해 이 프로시저를 반복하십시오.  

**팁:** 서버를 쉽게 식별할 수 있도록 하려면 동일한 풀 내의 서버에 대해 유사한 이름 지정 규칙(예: Web1, Web2, Web3 등)을 사용하십시오.

다음으로 서비스를 작성하십시오. 방금 입력한 각 서버에 대한 서비스를 작성합니다. 서비스는 NetScaler와 풀에 있는 서버 간의 연결을 구성하는 것입니다. 각 서비스에는 이름이 있으며 IP 주소, 포트 및 제공되는 데이터의 유형이 지정됩니다.

1. **Traffic Management > Load Balancing > Services**를 클릭하십시오.
2. **Add**를 클릭하십시오.
3. 동일한 정보를 활용하여 이전에 작성한 각 서버에 대한 서비스를 작성하십시오.

다음으로 가상 서버를 작성하십시오. 가상 서버는 이전에 작성한 로드 밸런싱된 서버 및 서비스에 사용되는 VIP 간 일종의 가상 연결입니다.

1. **Traffic Management > Load Balancing > Virtual Servers**를 클릭하십시오.
2. **Add**를 클릭하십시오.
3. 가상 서버의 Name을 지정하십시오.
4. 밸런싱할 Protocol(HTTP)을 지정하십시오.
5. IP Address Type을 기본값(IP Address)으로 두십시오. IP Address 필드는 모든 사용자의 시작점으로 사용할 VIP를 입력하는 위치입니다.
6. Port를 지정하십시오. 기본 포트는 80입니다.
7. **OK**를 클릭하십시오. 

이제 작성한 서비스를 가상 서버에 바인드하십시오.

1. Virtual Servers 화면에서 **No Load Balancing Virtual Server Service Binding** 링크를 클릭하십시오.
2. 이전에 작성한 각 서비스를 가상 서버에 바인드하십시오.
3. **Done**을 클릭하십시오.
4. **Refresh** 단추를 클릭하십시오. State 및 Effective State가 초록색으로 표시됩니다.

웹 사이트에 대한 로드 밸런싱 풀 및 정책을 작성했습니다.
