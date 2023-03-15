---

copyright:
  years: 2018, 2019
lastupdated: "2019-11-12"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Retrieve and transfer the certificate
{: #retrieve-and-transfer-the-certificate}

Retrieve the SSL certificate you ordered earlier so that you're ready for its installation and configuration in the step-by-step [Configuring and Tuning SSL Offload with {{site.data.keyword.vpx_full}}](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx).
{: shortdesc}

1. Shortly after validating ownership of the domain, you should receive an email confirming the completion of the certificate fulfillment and the certificate itself.

    Copy the text from `---BEGIN CERTIFICATE---` all the way to `---END CERTIFICATE---` and save the contents as a new certificate file with an extension of `.cer`.

2. Copy the certificate file to the `/nsconfig/ssl` directoy in the {{site.data.keyword.vpx_full}}.

The {{site.data.keyword.vpx_full}} is now ready to incorporate the certificate into a load balancing deployment using SSL.
