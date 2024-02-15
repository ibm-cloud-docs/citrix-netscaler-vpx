---

copyright:
  years: 2018, 2019
lastupdated: "2019-11-12"

keywords:

subcollection: citrix-netscaler-vpx


---

{{site.data.keyword.attribute-definition-list}}

# Check and configure the DNS record
{: #check-and-configure-the-dns-record}

In this step-by-step example, the DNS service from {{site.data.keyword.cis_full}} is used to manage the DNS zone and its records. In this case, you must ensure that a record is created for the FQDN being used. The record should point to the public address to be configured in the {{site.data.keyword.vpx_full}} virtual server.
{: shortdesc}

The static public IP to be used with the Citrix VPX can be retrieved from the IBM Cloud catalog from the [Device List](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#locating-netscaler-details-in-the-customer-portal) and then selecting the name of your {{site.data.keyword.vpx_full}}.
