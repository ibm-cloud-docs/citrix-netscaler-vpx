---

copyright:
  years: 2019
lastupdated: "2019-04-10"

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

# Creating an IP Tunnel
{: #creating-ip-tunnel}

You need to create an IP tunnel object to specify not only the local and remote IP addresses, but also the protocol parameters for the VPN connection. To do so:

1.	Navigate to **System > CloudBridge Connector > IP Tunnels**.
2.	On the **IPv4 Tunnels tab**, click **Add**.
3.	Enter the following parameters:
  *	Name
  *	Remote IP (IP of remote VPN peer)
  *	Remote Mask
4.	Select **Subnet IP** (SNIP) in the Local IP drop down list.
5.	Choose the appropriate SNIP to be used as the VPN endpoint from the **Local IP** drop down.
6.	Select **IPSEC** as the protocol from the drop down list.
7.	Choose the [previously created](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) profile name from the **IPSec Profile Name** drop down.
8.	Click **Create**.

    ![Create IP Tunnel](images/ipsecCreateIPtunnel.png)

To create an IP tunnel in the CLI, use the following syntax:

  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1

  ```
