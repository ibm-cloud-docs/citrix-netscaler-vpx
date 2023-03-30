---
copyright:
  years: 1994, 2017
lastupdated: "2022-05-04"

keywords: order, citrix, vpx, overview

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with Citrix Netscaler VPX
{: #getting-started}

Deploying a {{site.data.keyword.vpx_full}} in your IBM Cloud solution accelerates web application delivery, boosts performance, and ensures your cloud applications and services stay optimized, available, and secure. If you have challenging workloads, such as gaming, big data and analytics, or private clouds, the {{site.data.keyword.vpx_full}} can help you deliver your solution when, where, and how your users need it most.
{: shortdesc}

## Before you begin
{: #before-you-begin}

To get started with {{site.data.keyword.vpx_full}}, you will need to know the following information:

* Your IBM© Cloud catalog login information
* The deployment location for your load balancer
* Which Netscaler type best fits your needs (for more information refer to [Explore Load Balancers](/docs/citrix-netscaler-vpx?topic=loadbalancer-service-explore))
* The number of public IP addresses needed
* The VLAN where you want to assign the load balancer

To get the maximum value from your Citrix Netscaler VPX, make sure you allocate and apply your Citrix ADC licenses using the new Citrix licensing framework. For more information, refer to [Citrix ADC licensing overview](https://docs.citrix.com/en-us/citrix-adc/12-1/licensing/citrix-adc-licensing-overview.html){: external}
{: important}

## Ordering a {{site.data.keyword.vpx_full}}
{: #ordering-a-citrix-netscaler-vpx}

To order a {{site.data.keyword.vpx_full}} software appliance, navigate to the order page in the IBM Cloud catalog:

1. From your browser, open the [IBM Cloud catalog](/login){: external} and log into your account.
2. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the top left, then click **Classic Infrastructure**.
3. Click the **Order Devices** button.
4. In the Catalog page, scroll down to the Network section and click the **Load Balancer** tile.
5. Select {{site.data.keyword.vpx_full}}, then click **Create**.
6. Select a Location from the dropdown menu where you would like to deploy your {{site.data.keyword.vpx_full}} software appliance.  
7. Select the best NetScaler type for your software edition, software version and throughput needs.
8. Select the number of public IP addresses you need.  
   These are static public IP addresses, deployed as virtual IP addresses (VIPs) on your NetScaler VPX.
9. Click **Continue**.
10. Enter the information required by ARIN (or the equivalent organization in your region of deployment) for the IP addresses you've requested.
11. Enter your contact information.
12. Select your VLAN.
   To minimize latency and ensure optimized utilization of your network resources, assign the {{site.data.keyword.vpx_full}} to the same VLAN as the servers where the traffic will be distributed.
13. Review the order, accept the terms, and click **Place Order**. The {{site.data.keyword.vpx_full}} software appliance deploys with your selected settings.

## What's next
{: #what-s-next}

You can learn more about {{site.data.keyword.vpx_full}} [features](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-about-citrix-netscaler-vpx), review specific Netscaler [terminology](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-citrix-netscaler-vpx-terminology), or start [configuring](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-basic-load-balancing-configuration) your Netscaler.
