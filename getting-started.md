---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"

keywords: order, vpx, overview

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Getting started with Citrix NetScaler VPX Software Appliance
{: #getting-started}

Deploying a Citrix NetScaler VPX in your {{site.data.keyword.BluSoftlayer_notm}} solution accelerates web application delivery, boosts performance, and ensures your cloud applications and services stay optimized, available, and secure. If you have challenging workloads, such as gaming, big data and analytics, or private clouds, the Citrix NetScaler VPX can help you deliver your solution when, where, and how your users need it most.

## Before you begin
{: #before-you-begin}
To get started with Citrix NetScaler VPX, you will need to know the following information:

* Your IBM© Cloud Customer Portal login information
* The deployment location for your load balancer
* Which Netscaler type best fits your needs (for more information refer to [Explore Load Balancers](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)
* The number of public IP addresses needed
* The VLAN where you want to assign the load balancer

## Ordering a Citrix NetScaler VPX
{: #ordering-a-citrix-netscaler-vpx}

To order a Citrix NetScaler VPX software appliance, navigate to the order page in the Customer Portal:

1. From your browser, open  [Customer Portal ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} and log into your account.
2. In the Customer Portal navigation, select **Devices > Devices List** and click on the **Order Devices** link.
3. In the **Order SoftLayer Products and Services** page, scroll down to the Network section and click the **Order** link under Citrix NetScaler VPX.
4. Select a Location from the dropdown menu where you would like to deploy your Citrix NetScaler VPX software appliance.  
5. Select the best NetScaler type for your software edition, software version and throughput needs.
6. Select the number of public IP addresses you need.  
	These are static public IP addresses, deployed as virtual IP addresses (VIPs) on your NetScaler VPX.
7. Click **Continue**.
8. Enter the information required by ARIN (or the equivalent organization in your region of deployment) for the IP addresses you've requested.
9. Enter your contact information.
10. Select your VLAN.
	To minimize latency and ensure optimized utilization of your network resources, assign the Citrix NetScaler VPX to the same VLAN as the servers where the traffic will be distributed.
11. Review the order, accept the terms, and click **Place Order**. The Citrix NetScaler VPX software appliance deploys with your selected settings.

## What's Next
{: #what-s-next}

You can learn more about Citrix Netscaler VPX [features](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-about-citrix-netscaler-vpx), review specific Netscaler [terminology](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-citrix-netscaler-vpx-terminology), or start [configuring](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-basic-load-balancing-configuration) your Netscaler.
