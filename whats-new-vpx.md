---

copyright:
  years: 2017, 2025
lastupdated: "2025-04-03"

keywords: updates, additions, version

subcollection: citrix-netscaler-vpx

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for Citrix Netscaler VPX
{: #citrix-netscaler-vpx-release-notes}

You can see the latest updates and function enhancements for your {{site.data.keyword.vpx_full}} and IBM Cloud here.
{: shortdesc}

## 13 November 2019
{: #citrix-netscaler-vpx-nov1319}
{: release-note}

Virtual servers with multiple IP addresses
:    You can now create a single load balancing virtual server with multiple non-consecutive or consecutive VIP IPv4 and IPv6 addresses. Each VIP address bound to a virtual server is treated as an individual virtual server.

For more information about this feature, see the Citrix article [Multiple IP virtual servers](https://docs.netscaler.com/en-us/){: external}.

## 25 September 2018
{: #citrix-netscaler-vpx-sep2518}
{: release-note}

SSL
:    The following updates apply to SSL connections:
    * Removal of weak ciphers from the DEFAULT_BACKEND cipher group.
    * Support for ECDHE ciphers on the front end of Thales nShield® external HSM
    * Support for ECDHE ciphers on the front end of SafeNet network external HSM
    * Removal of SSLv2: The NetScaler VPX appliance does not support SSLv2 from release 12.1.

## 23 January 2018
{: #citrix-netscaler-vpx-jan2318}
{: release-note}

Service group support for GSLB
:    You can now configure IP address-based service groups, domain-name-based service groups, or domain-name-based autoscale service groups for GSLB. You can also manage a group of services as easily as a single service, and bind a service group to a virtual server, as well as add services to the group.
