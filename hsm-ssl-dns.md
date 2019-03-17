---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, dns, security, check, configure

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Check and Configure the DNS Record
{: #check-and-configure-the-dns-record}

In this Step by Step example, the DNS service from IBM© Cloud Internet Services is used to manage the DNS zone and its records. In this case, you must ensure a record is created for the FQDN being used. The record should point to the public address to be configured in the Citrix Netscaler VPX virtual server.

<img src="images/12-add-record.png" alt="drawing" style="width: 700px;"/>

The static public IP to be used with the Citrix VPX can be retrieved from the Customer Portal by navigating to **Devices > Device List** and then selecting the name of your Citrix Netscaler VPX.

<img src="images/13-check-ip.png" alt="drawing" style="width: 300px;"/>
