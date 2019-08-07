---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: subnet, private, request, vip

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

# Request a Private Subnet
{: #request-a-private-subnet}

In most deployments, the {{site.data.keyword.vpx_full}} appliance is deployed in a reverse-proxy configuration. However, to configure the VPX with a forward-proxy configuration, Virtual IPs (VIPs) are needed, since the configuration will exist on a private network instead of a public one.

You must open a ticket with the IBM© Cloud support team and request that a private network for your {{site.data.keyword.vpx_full}} appliance be added to your account. Note that you will require at least two private addresses, so you should request a private subnet size of at least /29.  
