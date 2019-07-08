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

# 创建 IPSec 概要文件 VPX
{: #creating-ipsec-profile}

IPSec 概要文件包含用于建立连接的安全参数。要创建概要文件，请执行以下过程：

1.	导航至**系统 > CloudBridge Connector > IPSec 概要文件**，然后单击**添加**。
2.	输入以下参数：
  *	**名称**
  *	**加密算法**
  *	**散列算法**
  *	**生命周期**
3.	选择相应的 **IKE 协议版本**。
4.	根据需要选中**完美前向保密**。
5.	选中**预共享密钥存在**，然后在**值**字段中输入 PSK。
6.	单击**创建**。

    <img src="images/ipsecCreateProfile.png" alt="图样" style="width: 200px;"/>

要在 CLI 中创建 IPSec 概要文件，请使用以下语法：
  
  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra
  
  ```
