---

copyright:
  years: 2019
lastupdated: "2019-03-28"

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

# Configuring IPSec Site-to-site VPN in Citrix NetScaler VPX
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

This guide provides step-by-step instructions to configure an IPSec VPN site-to-site connection in Citrix VPX. An IBM Virtual Router Appliance (VRA) will be used as VPN peer.

<img src="images/ipsec1.png" alt="drawing" style="width: 600px;"/>

## About the deployment
This deployment was built and tested with the following component specifications:

| NetScaler VPX Version & Build	| VRA Version & Description | 
| ------------- | ------------- | 
| NS12.1: Build 48.13.nc | AT&T vRouter 5600 1801q |

**NOTE:** You will need a VPX Platinum license to configure IPSec VPN.

## Before you begin

This guide assumes ownership of both devices, visit the following links for instructions on ordering these.

-	[Getting started with Citrix NetScaler VPX Software Appliance](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started-with-citrix-netscaler-vpx-software-appliance#getting-started-with-citrix-netscaler-vpx-software-appliance)
-	[Getting Started with IBM Virtual Router Appliance](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#getting-started-with-ibm-virtual-router-appliance){: new_window}

## What you'll accomplish

In this guide you will learn how to configure IPSec VPN in the Citrix VPX device.

Task  | Description
------------- | -------------
[Enable Required Features in VPX]() | First, enable the required features to create the IPSec VPN.
[Create IPSec Profile]() | The IPSec profile will include security parameters to be used for the establishment of the connection. 
[Create IP Tunnel]() | In this section we will create an IP tunnel object to specify local and remote IP address as well as protocol parameters.
[Create Policy Based Routing (PBR)]() | PBR will be used to indicate the interesting traffic parameters (local and remote subnets).
[Get VRA Configuration]() | VRA equivalent VPN configuration syntax.
[Verify VPN Status]() | Verify VPN operation state and conduct a simple connectivity test.

## Additional resources
The following additional resources can help learn more about Citrix VPX and VRA.

* [CloudBridge Connector ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configuring a CloudBridge Connector tunnel between a Citrix ADC appliance and Cisco IOS device ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Citrix VPX/ADC 12.1 Documentation](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [Supplemental VRA Documentation](https://console.bluemix.net/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}