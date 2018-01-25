---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

<a name="top"></a>
# FAQs

The following are frequently asked questions when working with the Citrix NetScaler VPX.

## What is Citrix NetScaler VPX?

Citrix NetScaler is an application delivery controller that makes applications five times better by accelerating performance, ensuring application availability and protection and substantially lowering operational costs. Choose the best Citrix NetScaler edition that meets your application requirements, and deploy it on the appropriate dedicated system for your performance needs. To learn more about Citrix NetScaler, refer to the [NetScaler page ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){: new_window}
 on the Citrix website.

## Why is load balancing needed?

Load balancing traffic has become a key aspect of many customer implementations as it distributes application requests and loads over multiple servers. It also provides a number of benefits to the overall topology including:

* Security. Logical isolation of the application servers is created or traffic requests denied based on IP protocols and port numbers.
* High-availability. Content is replicated to a pool, or group of servers, guaranteeing its availability to hosts.
* Scalability. Additional servers can be added as demand increases, enabling the load balancer to distribute the workload over the additional servers.
* Efficiency. Workloads are dynamically distributed when load balancing is configured. For example, resources like CPUs can be used in a more efficient ways.

## How many load balancing options are available in {{site.data.keyword.BluSoftlayer_notm}}?

For a detailed comparison of IBM's Load Balancer offerings, refer to [Explore Load Balancers](https://dev-console.bluemix.net/docs/infrastructure/loadbalancer-service/explore-load-balancers.html#explore-load-balancers).

## Does NetScaler support IPv6?

Yes. Both IPv6 and IPv4 are supported on the {{site.data.keyword.BluSoftlayer_notm}} public network.

## Will the NetScaler load balance traffic on the private network?

Yes, the NetScaler is the only {{site.data.keyword.BluSoftlayer_notm}} load balancing product that extends into the private network.

## Can the NetScaler be configured to report the client's source IP address instead of the source IP of the NetScaler appliance?

Yes, the **Use Source IP (USIP)** parameter can be set to **YES** within the NetScaler Advanced Management Interface to allow reporting of the client's source IP instead of that of the NetScaler.

Enabling the USIP address mode on the appliance adds flexibility to the appliance to use the client IP address, available in the IP header, when communicating to the server. By enabling this mode, the appliance opens server connections with the client IP address and also factors the client IP address in connection reuse. Therefore, this mode facilitates limited reuse per client based on client IP address.

## What are the various ports used to exchange the HA-related information between the nodes in an HA configuration?

Port 3010, for synchronization and command propagation. UDP Port 3003, to exchange heartbeat packets.

## What version of NetScaler VPX includes global server load balancing (GSLB)?

Platinum.

## Can I have NetScaler in HA configuration?

Yes, NetScaler VPX appliances support High Availability (HA) configurations.

NetScaler VPX servers are not redundant, unless configured in HA mode with a partner. As part of your back up and recovery strategy, it is highly recommended to deploy an HA environment when using NetScaler VPX.

It is also important to provide redundancy for other hardware and software components. For example, power supplies and local disk drives may not have redundancy. A failure in these components may result in data loss.

## Does the {{site.data.keyword.BluSoftlayer_notm}} NetScaler offering include SSL VPN functionality?

Yes, this feature is known as NetScaler Gateway™ and is included in all editions.  For more information regarding this feature please visit the [Citrix website ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.citrix.com/products/netscaler-adc/){: new_window}
