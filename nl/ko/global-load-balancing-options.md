---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 글로벌 로드 밸런싱

글로벌 서버 로드 밸런싱(GSLB)은 DNS 및 지리적 위치를 서버 트래픽이 전송되어야 하는 위치를 판별하는 방법으로 사용하여 여러 서버에 걸쳐 트래픽을 분할하는 메소드입니다. 일반적으로 글로벌 로드 밸런서는 클라이언트에 더 근접한 서버에 클라이언트 요청을 전송하여 대기 시간을 줄이고 성능을 향상시킵니다.

글로벌 로드 밸런싱 솔루션의 전체 구현이 필요하지 않을 수도 있습니다. GSLB에는 이 기능을 수행할 수 있는 적합한 디바이스의 다중 인스턴스가 필요하며 요구사항에 따라 다른 솔루션이 더 매력적일 수 있습니다. 전체 웹 사이트 및 애플리케이션이 필요한 경우 GSLB가 좋은 선택입니다. 이미지, 동영상 또는 기타 큰 파일과 같은 컨텐츠의 부분만 필요한 경우 [CDN(Content Delivery Network)](https://console.bluemix.net/docs/infrastructure/CDN/about.html#about-content-delivery-networks-cdn-){: new_window}이 더 적합하고 배치가 더 용이할 수 있습니다.

## Citrix NetScaler VPX

Citrix NetScaler VPX는 진정한 글로벌 로드 밸런싱을 수행하는 유일한 고객 구성 가능 디바이스입니다. NetScaler는 DNS 기반 글로벌 로드 밸런싱 검색을 수행할 수 있는 다기능 어플라이언스입니다. DNS 서버로 NetScaler를 지정할 수 있습니다. 그러면 디바이스가 로드 밸런싱하도록 구성된 서버를 검토하고 거리 계산을 수행하며 클라이언트 요청에 가장 근접한 서버의 IP가 포함된 레코드를 리턴합니다.

글로벌 로드 밸런싱 구성에서는 여러 데이터 센터에 다중 NetScaler 어플라이언스가 있으며 각각은 뒤에 있는 서버에 대한 로컬 로드 밸런싱 서비스를 제공합니다. 디바이스가 서로 통신하도록 구성되었으므로 글로벌 로드 밸런서 순환에 지정된 각 서버에 대한 상태 정보를 교환합니다. 이러한 구성된 NetScaler로 들어오는 모든 DNS 요청은 온라인 상태이며 응답성이 뛰어난 서버에 대한 적절한 레코드를 리턴할 수 있습니다. 응답하지 않는 서버는 순환에서 제거되고 다른 서버가 선택됩니다.

밸런싱 중인 유일한 서버인 경우에도 로드 밸런싱이 이미 설정되어 있어야 합니다. 일부 서비스의 경우 추가 IP 주소, 즉 GSLB 사이트 IP가 필요합니다. 이 IP는 NetScaler가 글로벌 로드 밸런싱 프로토콜에서 다른 NetScaler와 통신하는 데 사용됩니다. 

다음 글로벌 밸런싱 프로시저에서는 다음을 사용합니다.

### VPX1

`50.97.235.236`은 `VPX1Vserver`로 이름 지정되며 해당 디바이스에 대한 로컬 로드 밸런싱 VIP입니다. `50.23.66.52`는 `VPX1site`라고 하며 해당 디바이스의 GSLB에 대한 로컬 IP입니다.

### VPX2
`208.43.241.249`는 `VPX2Vserver`에 사용되고 GSLB IP는 `208.43.224.4`이며 `VPX2site`라고 합니다.

1. **Traffic Management > GSLB**로 이동하고 오른쪽 마우스 단추를 클릭하여 기능을 사용으로 설정하십시오. 그런 다음 **Sites** 및 **Add**를 선택하십시오.

2. 첫 번째 디바이스에서 Name을 VPX1로, Type을 local로, IP를 `50.23.66.52`로 입력한 후 **Close**를 선택하십시오. 

	나열된 사이트의 상태가 초록색으로 표시되어야 합니다. 원격 사이트를 아직 추가하지 마십시오.

3. **Traffic Management > GSLB**로 이동하여 **GSLB Wizard**를 선택하십시오. **Next**를 클릭하십시오. 로드 밸런싱될 호스트 이름(이 예에서는 `gslb.tsstesting.com`)을 입력하십시오. Record Type을 A로, Service Type을 ANY로 두십시오. 가상 서버 이름이 자동으로 채워집니다. **Next**를 클릭하십시오.

4. 일반 로드 밸런싱의 경우와 마찬가지로 밸런싱 및 지속성 메소드의 양식을 선택하십시오. **Next**를 클릭하십시오.

5. 사이트가 이미 채워져 있으므로 항목을 추가할 필요가 없습니다. 대신 첫 번째 사이트의 이름 옆에 있는 초록색 '+'를 클릭하십시오. 목록에서 해당 디바이스의 vserver를 선택하고 **Create**를 클릭하십시오. 사이트가 로드 밸런싱된 설정의 사이트 IP 및 vserver IP로 구성되었으며 초록색으로 표시되어야 합니다. **Next**, **Finish** 및 **Exit**를 클릭하십시오.

6. 해당 서버에 대한 값을 사용하여 다음 NetScaler에 대해 동일한 조치를 수행하십시오.

7. 두 서버 모두에서 **Traffic Management > DNS > Records > A records**로 이동하여 목록을 검사하십시오. GSLB DOMAIN 유형으로 `root.servers.net` 항목과 호스트 이름이 표시되어야 합니다. 

8. **Traffic Management > DNS > Name Servers**로 이동하여 **Add**를 클릭하십시오. NetScaler의 IP 주소(예: 디바이스의 공인 IP)를 입력하십시오. **Local**을 클릭하고 프로토콜을 UDP로 두십시오. **Create**를 클릭한 후 **Close**를 클릭하십시오. 유효 상태가 enabled 및 up으로 표시되어야 합니다.

9. **System > Network > IPs**로 이동하여 GSLB IP 주소를 여십시오. 두 시스템 모두에 대해 **Management**가 선택되었는지 확인하십시오.

10. 다음으로 두 서버 모두에서 **Traffic Management > GSLB**로 되돌아가서 마법사를 다시 진행하십시오. 이때 **Next**를 클릭하고 **Modify Configuration for Existing Domains**를 선택하십시오. 목록에서 호스트 이름을 선택한 후 **Next**를 두 번 클릭하십시오. 

11. 사이트 주소 필드에 다른 NetScaler의 사이트 IP 주소를 입력한 후 다른 NetScaler의 사이트 이름을 지정하고 **Add**를 클릭하십시오. 초록색 '+'를 다시 클릭하는 옵션으로 사이트가 채워집니다. 다른 사이트를 추가하려면 원격 사이트 더하기 부호를 클릭하십시오. vserver 서비스 IP(GSLB 사이트 IP가 아니라 로드 밸런싱된 서버용 IP) 및 포트를 입력하고 **Create**, **Close**, **Next**, **Finish**를 클릭한 후 **Exit**를 클릭하십시오.

이 시점까지 모든 항목이 작동하고 두 서버가 모두 구성된 경우 GSLB 가상 서버, 서비스 및 사이트에서 모든 항목의 상태가 초록색이어야 합니다. 올바르게 동기화된 경우 이제 두 시스템 모두에서 GSLB 서비스에 두 개의 항목이 있음을 알 수 있습니다. 이 시점에서는 서버가 서로 통신 중입니다.

이제 DNS를 구성해야 합니다.

이 `gslb.tsstesting.com` 예에서는 tsstesting.com 구역에 NS 및 글루 레코드를 작성할 수 있습니다.

    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; nameserver IP of first NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; nameserver IP of second NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias to the GSLB object on the NetScaler appliance

도메인의 루트가 아니라 호스트 이름을 포함하는 CNAME만 사용할 수 있음을 기억하십시오.

이 구성은 `gslb.tsstesting.com`에 대한 요청의 이름 서버를 DNS를 구성한 NetScaler IP로 설정합니다. CNAME 레코드는 `tsstesting.com`을 `gslb.tsstesting.com`에 대한 요청으로 변환합니다. 그런 다음 `www.tsstesting.com`에 대한 모든 요청이 분석되기 위해 NetScaler로 이동하고 구성한 로드 밸런싱 메소드를 기반으로 레코드를 리턴합니다.

NetScaler 글로벌 로드 밸런싱에 대한 자세한 정보는 다음을 참조하십시오.
* [글로벌 로드 밸런싱을 위해 Netscaler 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://support.citrix.com/article/CTX110348){: new_window}
* [DNS(Domain Name System)가 NetScaler의 GSLB 기능과 함께 작동하는 방법 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://support.citrix.com/article/CTX122619){: new_window}
* [MEP 프로토콜 및 사이트 모니터링에 대한 정보![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://support.citrix.com/article/CTX111081){: new_window}

다음은 지리적 기준에 따라 트래픽을 분산하기 위해 유사한 기능을 제공할 수 있는 다른 제품들입니다.

### CDN

CDN(Content Delivery Network)을 사용하면 원래 서버를 지리적으로 분산된 캐시 서버에 업로드하거나 제공한 후 요청 클라이언트에 컨텐츠를 제공할 수 있습니다. CDN은 시간이 경과함에 따라 변경되지 않는 이미지 및 동영상과 같은 정적 대량 컨텐츠에서 가장 잘 작동합니다.

CDN에 대한 세부사항은 [문서](https://console.bluemix.net/docs/infrastructure/CDN/getting-started.html#getting-started)를 참조하십시오.

### 오브젝트 스토리지

다양한 데이터 센터의 여러 지리적 위치를 사용하여 컨텐츠를 제공하도록 {{site.data.keyword.BluSoftlayer_notm}}의 오브젝트 스토리지를 구성할 수 있습니다. 지리적으로 인식 가능한 애플리케이션이 클라이언트 요청에 대한 위치 검색을 수행하고 클라이언트에 근접한 오브젝트 스토리지에 URL을 리턴할 수 있습니다. 위에서 언급한 대로 필요한 경우 추가 캐싱 서비스를 제공하기 위해 오브젝트 스토리지는 CDN 프론트 엔드와 함께 제공됩니다.

자세한 정보와 오브젝트 스토리지에 대한 소개는 [문서](https://console.bluemix.net/docs/services/cloud-object-storage/about-cos.html#about-ibm-cos)를 참조하십시오. 
