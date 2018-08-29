---
copyright:
  years: 1994, 2018
  
lastupdated: "2018-08-29"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# What's New in Citrix NetScaler VPX 12.1

## Networking

* Virtual servers with multiple IP addresses: You can create a single load balancing virtual server with multiple non-consecutive/consecutive IPv4 and IPv6 addresses of type VIP. Each VIP address bound to a virtual server is treated as an individual virtual server.

For more information about this feature, see [Multiple IP virtual servers ![External link icon](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}.

## SSL
 
* Removal of weak ciphers from the DEFAULT_BACKEND cipher group. 
* Support for ECDHE ciphers on the front end of Thales nShield® external HSM
* Support for ECDHE ciphers on the front end of SafeNet network external HSM
* Removal of SSLv2: The NetScaler VPX appliance does not support SSLv2 from release 12.1.

For more details about 12.1 SSL updates, see [Citrix 12.1 Release Note ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}.

## GSLB

* Service Groups Support for GSLB: You can configure IP address-based service groups, domain name-based service groups, or domain name-based autoscale service groups for GSLB. You can manage a group of services as easily as a single service, and bind a service group to a virtual server, and add services to the group.

For more information about GSLB service groups, see [Multiple IP virtual servers ![External link icon](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}.







