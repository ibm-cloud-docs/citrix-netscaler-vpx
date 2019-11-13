---

copyright:
  years: 2018
lastupdated: "2019-11-12"

keywords: hsm, security, retrieve, transfer, certificate

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

# Retrieve and Transfer the Certificate
{: #retrieve-and-transfer-the-certificate}

Retrieve the SSL certificate you ordered earlier so that you're ready for its installation and configuration in the next Step by Step, [Configuring and Tuning SSL Offload with {{site.data.keyword.vpx_full}}](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx).
{: shortdesc}

1. Shortly after validating ownership of the domain, you should receive an email confirming the completion of the certificate fulfillment and the certificate itself.

	Copy the text from `---BEGIN CERTIFICATE---` all the way to `---END CERTIFICATE---` and save the contents as a new certificate file with an extension of `.cer`.

2. Copy the certificate file to the `/nsconfig/ssl` directoy in the {{site.data.keyword.vpx_full}}.

  ![Transfer Certificate](images/11-transfer-certificate.png)

The {{site.data.keyword.vpx_full}} is now ready to incorporate the certificate into a load balancing deployment using SSL.
