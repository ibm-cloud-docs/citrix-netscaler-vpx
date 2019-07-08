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

# IPSec プロファイル VPX の作成
{: #creating-ipsec-profile}

IPSec プロファイルには、接続を確立するためのセキュリティー・パラメーターが含まれています。プロファイルを作成するには、以下の手順を実行します。

1.	**「System」>「CloudBridge Connector」>「IPSec Profile」**とナビゲートし、**「Add」**をクリックします。
2.	次のパラメーターを入力します。
  *	**Name**
  *	**Encryption Algorithm**
  *	**Hash Algorithm**
  *	**Lifetime**
3.	適切な**「IKE Protocol Version」**を選択します。
4.	必要に応じて、**「Perfect Forward Secrecy」**にチェック・マークを付けます。
5.	**「Pre-Shared Key Exists」**にチェック・マークを付け、**「Value」**フィールドに PSK と入力します。
6.	**「Create」**をクリックします。

    <img src="images/ipsecCreateProfile.png" alt="図" style="width: 200px;"/>

CLI で IPSec プロファイルを作成するには、次の構文を使用します。
  
  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra
  
  ```
