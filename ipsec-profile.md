---

copyright:
  years: 2019
lastupdated: "2019-11-13"

keywords: ipsec, vpn, vpx, tunnel

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank_"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Creating IPSec Profile VPX
{: #creating-ipsec-profile}

You an create an IPSec profile that includes security parameters for establishing connections with your {{site.data.keyword.vpx_full}}.
{: shortdesc}

To create a profile, perform the following procedure:

1.	Navigate to **System > CloudBridge Connector > IPSec Profile** and click **Add**.
2.	Enter the following parameters:
  *	**Name**
  *	**Encryption Algorithm**
  *	**Hash Algorithm**
  *	**Lifetime**
3.	Select the appropriate **IKE Protocol Version**.
4.	Check **Perfect Forward Secrecy** if desired.
5.	Check **Pre-Shared Key Exists** and enter the PSK in the **Value** field.
6.	Click **Create**.

    ![Create IPSec Profile](images/ipsecCreateProfile.png)

To create an IPSec profile in the CLI, use the following syntax:

  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra

  ```
