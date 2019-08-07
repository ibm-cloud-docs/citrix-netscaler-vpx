---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: nat, traffic, configure, configuration

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

# Configure Source NAT for Outbound Traffic
{: #configure-source-nat-for-outbound-traffic}

Network address translation (NAT) is a method of remapping one IP address space into another by modifying network address information in the IP header of packets while they are in transit across a traffic routing device.

You may utilize your {{site.data.keyword.vpx_full}} appliance to perform NAT on outbound traffic from your client machines. To do so:

1. Go to System > Network > Routes, and navigate to the **RNAT** tab. Click **Configure RNAT**.

2. Specify the source subnet (and mask) to which you wish to apply RNAT and click **OK**.

The Internet-bound traffic sourced from any IP in this subnet will now use NAT for tradfic on the Citrix NetScaler’s public IP address.    
