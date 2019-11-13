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

# Creating Policy Based Routing (PBR)
{: #creating-policy-based-routing}

A Policy Based Routing (PBR) policy is needed to specify the unique traffic parameters (such as local and remote subnets) the VPN connection will use with your {{site.data.keyword.vpx_full}}.
{: shortdesc}

To create a PBR profile perform the following steps:

1.	Navigate to **System > Network > PBR** and select **Add**.
2.	Enter **Name**.
3.	Leave **Action** as the default setting **ALLOW**.
4.	For **Next Hop Type**, select **IP Tunnel**, then pick the [previously created](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) tunnel from the **IP Tunnel Name** drop down list.
5.	Ensure you have checked **Enable PBR**.
6.	In the **Configure IP** section, select **=** for the **Operation** field, for both source and destination.
7.	Specify the first and last subnet IP in the following fields:
  *	**Source IP Low**
  *	**Source IP High**
  *	**Destination IP Low**
  *	**Destination IP High**
8.	Click **Create**.
9.	From **System > Network > PBRs**, select the new PBR, click the **Select Action** list, then choose **Apply**.

To create the PBR profile in the CLI, use the following syntax:

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs

  ```
  {: codeblock}

  Be advised that any virtual server instances or infrastructure intended to go through the VPN tunnel and sit behind the VPX, will need to be configured to either use VPX as the default gateway or to use a static route. This will send traffic to the VPX when the destination is the remote (peer) subnet. See the static route (**10.115.0.0/16**) example below.
  {: note}

  ```
  >route print
  ===========================================================================
  Interface List
  3...06 93 7a 03 f0 b3 ......XenServer PV Network Device #0
  4...06 ff 8f 6d 89 e8 ......XenServer PV Network Device #1
  1...........................Software Loopback Interface 1
  7...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
  10...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
  ===========================================================================

  IPv4 Route Table
  ===========================================================================
  Active Routes:
  Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0    169.54.255.65    169.54.255.73     26
       10.115.0.0      255.255.0.0      192.168.0.1      192.168.0.2     26

  ```
  {: codeblock}
