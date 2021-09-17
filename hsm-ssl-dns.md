---

copyright:
  years: 2018, 2019
lastupdated: "2019-11-12"

keywords:

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"} 
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic”}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Check and configure the DNS record
{: #check-and-configure-the-dns-record}

In this step-by-step example, the DNS service from {{site.data.keyword.cis_full}} is used to manage the DNS zone and its records. In this case, you must ensure a record is created for the FQDN being used. The record should point to the public address to be configured in the {{site.data.keyword.vpx_full}} virtual server.
{: shortdesc}

![Add record](images/12-add-record.png)

The static public IP to be used with the Citrix VPX can be retrieved from the IBM Cloud catalog from the [Device List](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#locating-netscaler-details-in-the-customer-portal) and then selecting the name of your {{site.data.keyword.vpx_full}}.

![Check IP](images/13-check-ip.png)
