---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX Default Deployment

When you view your NetScaler in **Devices > Device List** on the [Customer Portal ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/), you may notice that it looks different than other servers. Namely, the device has a Private IP address but no Public IP address.

The default deployment of a NetScaler at {{site.data.keyword.BluSoftlayer_notm}} is designed to be as secure as possible, by automatically assigning a Private IP address as the NetScaler IP (NSIP) used for management purposes. If you click the arrow to the left of the NetScaler, the line expands to show the default username (root) and the masked root user password. 

{{site.data.keyword.BluSoftlayer_notm}} handles a lot of the decisions for you during provisioning. For example, which IP addresses to use for which purposes. It asks which VLANs you would like to use for deployment. Also, it automates much of the back-end configuration using scripts and an API, such as assigning interfaces to separate public and private VLANs, and assigning the proper IP addresses to each interface, including the NSIP, VIPs, and SNIPs.

## What do I need to configure?

By default, the NSIP is the Private IP address assigned during provisioning, which is the IP address that you use to connect to the NetScaler for management purposes. The SNIPs (SubNet IP Addresses), by default, are assigned from the same Primary IP SubNets that are located on the VLANs that you chose during the ordering process. 

If you chose the same VLANs where your intended load-balanced servers reside, then no extra configuration of these SNIPs is necessary. By default, the DNS is set to {{site.data.keyword.BluSoftlayer_notm}}'s name servers. In a basic implementation, if {{site.data.keyword.BluSoftlayer_notm}} hosts the DNS records for your servers, then no further configuration is necessary.