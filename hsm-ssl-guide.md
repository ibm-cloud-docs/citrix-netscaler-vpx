---

copyright:
  years: 2018
lastupdated: "2019-11-12"

keywords: hsm, security, configure, tune, tuning, ssl, offload

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

# Configuring and tuning SSL Offload with Citrix Netscaler VPX
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

This Step by Step guides you through configuring and tuning SSL Offload in {{site.data.keyword.vpx_full}}, this is done by using the certificate and cryptographic material generated using the Hardware Security Monitor (HSM) link.
{: shortdesc}

This Step by Step assumes you have completed the steps in [Deploying and Configuring the IBM© Hardware Security Module (HSM) with {{site.data.keyword.vpx_full}}](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) to order and create your VPX/HSM pairing.
{: note}

## About the deployment
{: #about-deployment}
This deployment was built and tested with the following component specifications:

| NetScaler VPX Version & Build	| HSM Software Version | HSM Firmware version | HSM Client Version |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## Logical topology
{: #logical-topology}

The below diagram shows the network traffic flow for the SSL offload use case. This provides a visual and logical perspective of the trust link and the configuration between the Citrix VPX and the HSM appliance.

![Network flows logical topology](images/network-flows-logical-topology.jpg)

If you are not familiar with SSL offload, review this [Citrix article ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}.

## What you'll accomplish
{: #what-accomplish}

In this Step-by-Step guide you will learn how to configure SSL for a {{site.data.keyword.vpx_full}}:

Task  | Description
------------- | -------------
[Install the certificate](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) | Install the SSL Certificate you created in the previous [Step by Step](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx).
[Check and configure the DNS record](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | Ensure a DNS record exists for the FQDN that points to the public address to be configured in the {{site.data.keyword.vpx_full}} as a Virtual Server.
[Add and configure the SSL Virtual Server](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | Add and configure an SSL Virtual Server.
[Create and apply a new Cipher Suite](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | Create a Cipher Suite that prioritizes and preferences AEAD, ECDHE, and ECDSA.

## Additional resources
{: #additional-resources}
The following additional resources can help you get the most out of your {{site.data.keyword.vpx_full}} when using the IBM Hardware Security Module.

* [NetScaler 12.1 Product Documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Gemalto Support Portal ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [IBM Cloud Support](/docs/get-support?topic=get-support-using-avatar){:new_window}
