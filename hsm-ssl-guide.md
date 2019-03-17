---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, configure, tune, tuning, ssl, offload

subcollection: citrix-netscaler-vpx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configuring and Tuning SSL Offload with Citrix Netscaler VPX
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

This Step by Step guides you through configuring and tuning SSL Offload in Citrix Netscaler VPX, this is done by using the certificate and cryptographic material generated via the HSM link.

**NOTE:** This Step by Step assumes you have completed the steps in [Deploying and Configuring the IBM© Hardware Security Module (HSM) with Citrix Netscaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) to order and create your VPX/HSM pairing.

## About the deployment
This deployment was built and tested with the following component specifications:

| NetScaler VPX Version & Build	| HSM Software Version | HSM Firmware version | HSM Client Version |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## Logical topology
The below diagram shows the network traffic flow for the SSL offload use case. This provides a visual and logical perspective of the trust link and the configuration between the Citrix VPX and the HSM appliance.

<img src="images/network-flows-logical-topology.jpg" alt="drawing" style="width: 700px;"/>

If you are not familiar with SSL offload, review this [Citrix article ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}.

## What you'll accomplish

In this Step-by-Step guide you will learn how to configure SSL for a Citrix Netscaler VPX:

Task  | Description
------------- | -------------
[Install the certificate](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) | Install the SSL Certificate you created in the previous [Step by Step](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx).
[Check and configure the DNS record](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | Ensure a DNS record exists for the FQDN that points to the public address to be configured in the Citrix Netscaler VPX as a Virtual Server.
[Add and configure the SSL Virtual Server](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | Add and configure an SSL Virtual Server.
[Create and apply a new Cipher Suite](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | Create a Cipher Suite that prioritizes and preferences AEAD, ECDHE, and ECDSA.

## Additional resources
The following additional resources can help you get the most out of your Citrix Netscaler VPX when using the IBM Hardware Security Module.

* [NetScaler 12.1 Product Documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Gemalto Support Portal ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [IBM Cloud Support](https://{DomainName}/docs/get-support?topic=get-support-using-avatar){:new_window}
