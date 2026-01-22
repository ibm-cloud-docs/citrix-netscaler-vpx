---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-22"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Retrieve and transfer the certificate
{: #retrieve-and-transfer-the-certificate}

Retrieve the SSL certificate that you ordered earlier so that you're ready for its installation and configuration in the step-by-step [Configuring and Tuning SSL Offload with {{site.data.keyword.vpx_full}}](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx).
{: shortdesc}

1. After you validate ownership of the domain, you receive an email confirming the completion of the certificate fulfillment and the certificate itself.

    Copy the text from `---BEGIN CERTIFICATE---` all the way to `---END CERTIFICATE---` and save the contents as a new certificate file with an extension of `.cer`.

2. Copy the certificate file to the `/nsconfig/ssl` directory in the {{site.data.keyword.vpx_full}}.

The {{site.data.keyword.vpx_full}} is now ready to incorporate the certificate into a load balancing deployment by using SSL.
