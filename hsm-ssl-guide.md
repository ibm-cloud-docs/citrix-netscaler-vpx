---

copyright:
  years: 2018
lastupdated: "2018-11-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configuring and Tuning SSL Offload with Citrix Netscaler VPX
This Step by Step guides you through configuring and tuning SSL Offload in Citrix Netscaler VPX, this is done by using the certificate and cryptographic material generated via the HSM link.

**NOTE:** This Step by Step assumes you have completed the steps in [Deploying and Configuring the IBM Hardware Security Module (HSM) with Citrix Netscaler VPX](hsm-guide.html) to order and create your VPX/HSM pairing. 

## About the deployment
This deployment was built and tested with the following component specifications:

| NetScaler VPX Version & Build	| HSM Software Version | HSM Firmware version | HSM Client Version |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## Logical topology
The below diagram shows the network traffic flow for the SSL offload use case. This provides a visual and logical perspective of the trust link and the configuration between the Citrix VPX and the HSM appliance. 

<img src="images/network-flows-logical-topology.jpg" alt="drawing" style="width: 700px;"/>

If you are not familiar with SSL offload, review this [Citrix article](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html).

## What you'll accomplish

In this Step-by-Step guide you will learn how to configure SSL for a Citrix Netscaler VPX:

Task  | Description
------------- | -------------
[Install the certificate](hsm-ssl-install.html) | Install the SSL Certificate you created in the previous [Step by Step](hsm-order-certificate.html). 
[Check and configure the DNS record](hsm-ssl-dns.html) | Ensure a DNS record exists for the FQDN that points to the public address to be configured in the Citrix Netscaler VPX as a Virtual Server.
[Add and configure the SSL Virtual Server](hsm-ssl-server.html) | Add and configure an SSL Virtual Server.
[Create and apply a new Cipher Suite](hsm-ssl-cipher.html) | Create a Cipher Suite that prioritizes and preferences AEAD, ECDHE, and ECDSA.

## Additional resources
The following additional resources can help you get the most out of your Citrix Netscaler VPX when using the IBM Hardware Security Monitor.

* [NetScaler 12.1 Product Documentation](https://docs.citrix.com/en-us/netscaler/12-1/)
* [Gemalto Support Portal](https://supportportal.gemalto.com/csm?id=csm_index)
* [IBM Cloud Support](/docs/get-support/howtogetsupport.html#getting-customer-support)
