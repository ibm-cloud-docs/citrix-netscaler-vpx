---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX 업그레이드 
{: #upgrading-your-citrix-netscaler-vpx}

**참고:** 이 프로시저를 시도하기 전에 VPN에 연결되어 있어야 합니다.

1. NetScaler 관리 IP에 로그인하십시오.
2. **System Upgrade**를 클릭하십시오.
4. **Choose File** 드롭 다운 목록에서 **Local**을 선택하십시오. 
4. 다음 위치에서 올바른 업그레이드 파일을 다운로드하십시오.

	[사용 가능한 NetScaler 버전 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}
	
	**참고:** 이 링크에 액세스하려면 IBM© Cloud 인프라 VPN에 연결되어 있어야 합니다.

5. Upload Software 화면에서 업그레이드 파일의 위치를 찾아 이동하고 **Upgrade**를 클릭하십시오. 펌웨어가 업로드됩니다.
6. 결과 System Upgrade 창에서 다시 부팅하라는 메시지가 표시됩니다. **Close**를 클릭하십시오.
7. **System**으로 돌아가 **Reboot**를 클릭하십시오.
8. 업그레이드가 완료되면 어플라이언스에 액세스하기 전에 모든 브라우저 인스턴스를 닫고 컴퓨터의 캐시를 지우십시오.

**참고:** 

* 사용자 인터페이스는 사용자의 NetScaler VPX의 현재 버전에 따라 다를 수 있습니다.
* NetScaler 버전 11에서 버전 12로 업그레이드하는 경우 특히 설치 전 및 설치 중에 콜홈 기능을 사용 안함으로 설정해도 기본적으로 콜홈 기능이 사용으로 설정됩니다. 이 기능을 사용 안함으로 설정하려면 명령행 또는 Citrix 관리 UI를 사용할 수 있습니다. 
    
   * 명령행: `disable feature CallHome`
   * Citrix 관리 UI: 
     
     1. **구성** > **시스템** > **설정**으로 이동하십시오.
     2. 세부사항 분할창에서 **고급 기능 구성** 링크를 클릭하고 **콜홈** 옵션을 선택 취소하십시오.
     3. **OK**를 클릭하십시오.
