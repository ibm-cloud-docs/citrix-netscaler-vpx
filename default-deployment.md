---
copyright:
  years: 2017, 2026
lastupdated: "2026-01-21"

keywords:

subcollection: citrix-netscaler-vpx
---

{{site.data.keyword.attribute-definition-list}}

# Citrix Netscaler VPX default deployment
{: #citrix-netscaler-vpx-default-deployment}

{{site.data.keyword.vpx_full}} is securely deployed by automatically assigning a private IP address as the NetScaler IP (NSIP) used for management purposes.
{: shortdesc}

When you view your NetScaler in the [Device List](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#locating-netscaler-details-in-the-customer-portal) in the IBM Cloud catalog, it looks different than other servers. Namely, the device has a private IP address but no public IP address.

If you click the arrow to the left of the NetScaler, the line expands to show the default username (root) and the masked root user password.

IBM Cloud handles many of the decisions for you during provisioning. For example, which IP addresses to use for which purposes. It asks which VLANs you want to use for deployment. Also, it automates much of the back-end configuration with scripts and an API. Examples of this automation include assigning interfaces to separate public and private VLANs, and assigning the proper IP addresses to each interface, including the NSIP, VIPs, and SNIPs.

## What do I need to configure?
{: #what-do-i-need-to-configure-}

By default, the NSIP is the private IP address that is assigned during provisioning, which is the IP address that you use to connect to the NetScaler for management purposes. The SNIPs (SubNet IP addresses), by default, are assigned from the same primary IP SubNets that are on the VLANs that you chose during the ordering process.

If you chose the same VLANs where your intended load-balanced servers reside, then no extra configuration of these SNIPs is necessary. By default, the DNS is set to IBM Cloud name servers. In a basic implementation, if IBM Cloud hosts the DNS records for your servers, then no further configuration is necessary.
