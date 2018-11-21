---
copyright:
  years: 1994, 2018
  
lastupdated: "2018-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# What's New in Citrix NetScaler VPX

## Version 12.1

### Virtual servers with multiple IP addresses
You can now create a single load balancing virtual server with multiple non-consecutive/consecutive VIP IPv4 and IPv6 addresses. Each VIP address bound to a virtual server is treated as an individual virtual server.

For more information about this feature, see the Citrix article [Multiple IP virtual servers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}.

### SSL
The following updates have been applied for SSL connections:
 
* Removal of weak ciphers from the DEFAULT_BACKEND cipher group. 
* Support for ECDHE ciphers on the front end of Thales nShield® external HSM
* Support for ECDHE ciphers on the front end of SafeNet network external HSM
* Removal of SSLv2: The NetScaler VPX appliance does not support SSLv2 from release 12.1.

For more details about 12.1 SSL updates, see the [Citrix 12.1 Release Notes ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}.

### Service Groups Support for GSLB
You can now configure IP address-based service groups, domain-name-based service groups, or domain-name-based autoscale service groups for GSLB. You can also manage a group of services as easily as a single service, and bind a service group to a virtual server, as well as add services to the group.

For more information about GSLB service groups, see the Citrix article [Configuring a GSLB service group ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}.
