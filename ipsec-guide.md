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

# Configuring IPSec Site-to-site VPN in Citrix NetScaler VPX with IBM Virtual Router Appliance
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

This guide provides step-by-step instructions to configure an IPSec VPN site-to-site connection in Citrix VPX. An IBM Virtual Router Appliance (VRA) is used as a VPN peer.

<img src="images/ipsec1.png" alt="drawing" style="width: 600px;"/>

## About the deployment
This deployment was built and tested with the following component specifications:

| NetScaler VPX Version & Build	| VRA Version & Description | 
| ------------- | ------------- | 
| NS12.1: Build 48.13.nc | AT&T vRouter 5600 1801q |

You need a VPX Platinum license to configure IPSec VPN.
{: note}

## Before you begin

This guide assumes ownership of both devices. Please visit the following links for instructions on ordering.

-	[Getting started with Citrix NetScaler VPX Software Appliance](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[Getting Started with IBM Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## What you'll accomplish

In this guide you will learn how to configure an IPSec VPN in the Citrix VPX device.

Task  | Description
------------- | -------------
[Enable Required Features in VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) | First, enable the required features to create the IPSec VPN.
[Create IPSec Profile](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile) | The IPSec profile includes security parameters for establishing the connection. 
[Create IP Tunnel](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) | In this section we create an IP tunnel object to specify both local and remote IP addresses, as well as protocol parameters.
[Create Policy Based Routing (PBR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing) | PBR is used to define the unique traffic parameters for both local and remote subnets.
[Configure VRA](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra) | Configure the Virtual Router Appliance, using equivalent VPN configuration syntax.
[Verify VPN Status](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection) | Verify the VPN operation state and conduct a simple connectivity test.

## Additional resources
The following additional resources can help you learn more about Citrix VPX and Virtual Router Appliance.

* [CloudBridge Connector ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configuring a CloudBridge Connector tunnel between a Citrix ADC appliance and Cisco IOS device ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Citrix VPX/ADC 12.1 Documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [Supplemental VRA Documentation](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
