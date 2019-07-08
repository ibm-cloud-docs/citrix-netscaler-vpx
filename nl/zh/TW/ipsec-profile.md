---

copyright:
  years: 2019
lastupdated: "2019-04-28"

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

# 建立 IPSec 設定檔 VPX
{: #creating-ipsec-profile}

IPSec 設定檔包含用於建立連線的安全參數。若要建立設定檔，請執行下列程序：

1.	導覽至**系統 > CloudBridge Connector > IPSec 設定檔**，然後按一下**新增**。
2.	輸入下列參數：
  *	**名稱**
  *	**加密演算法**
  *	**雜湊演算法**
  *	**生命期限**
3.	選取適當的 **IKE 通訊協定版本**。
4.	根據需要勾選**完整轉遞保密**。
5.	勾選**預先共用金鑰存在**，然後在**值**欄位中輸入 PSK。
6.	按一下**建立**。

    <img src="images/ipsecCreateProfile.png" alt="圖片" style="width: 200px;"/>

若要在 CLI 中建立 IPSec 設定檔，請使用下列語法：
  
  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra
  
  ```
