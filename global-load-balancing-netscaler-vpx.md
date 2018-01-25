---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Global Load Balancing with Citrix NetScaler VPX

Global server load balancing (GSLB) is a mechanism to distribute traffic across multiple servers/instances, typically residing in different geographical locations. The idea is to have a global balancing engine/server that receives traffic requests from clients and redirects them to a certain geography, the latter determined using the criteria/algorithms selected and configured by the administrator. To achieve this, two recognized methods can be used inside the {{site.data.keyword.BluSoftlayer_notm}} network:

* **CDN:** Content Delivery Network (CDN) issued to deliver content and rich media such as images and videos, CDN distributes content geographically over dispersed nodes while keeping the least latency and highest speeds. It is usually implemented when particular portions of content need to be distributed as opposed to entire websites/applications. {{site.data.keyword.BluSoftlayer_notm}} offers this service, read more about it [here](https://console.bluemix.net/docs/infrastructure/CDN/getting-started.html#getting-started). 
* **NetScaler VPX:** Just like with regular local load balancing, VPX uses a similar object hierarchy to load balance traffic between several geographies. Using DNS based global lookups, NetScaler chooses the respective record that corresponds to the location/site selected, the selection is based on the criteria pre-configured by the administrator. The incoming sections will expand on this option/offering.

Note that other techniques are available for content distribution, such as HTTP redirection, that can also be implemented with the Citrix NetScaler VPX. 

## About GSLB on VPX

NetScaler VPX can be enabled with GSLB simply by activating its feature on the CLI/GUI. 

GSLB uses very similar components/objects as those used on local load balancing deployments, where entities are defined using a hierarchical model.

GSLB might be implemented for a number of purposes. Some of these could be:

* **Load sharing/distribution:** To distribute resources efficiently and smartly between multiple locations.
* **Disaster recovery:** Used when the main or primary location goes down or is unable to render the service. In this scenario an alternate/backup location can take over.
* **Performance/shaping:** This allows you to position content closer to end systems, or in a way that enhances the service in question.

The main components or entities in the GSLB process/deployment are:

* **Virtual servers:** A VIP is an IP address to which clients send requests, NetScaler terminates the client connection at the VIP and then it initiates a connection with a server configured in the (local) load balancing service. 
* **DNS (Domain Name System) and Name servers:** Name resolution on GSLB works very much like regular DNS. The difference is the logic/criteria used to determine the address(es) resolved, GSLB uses a pre-configured load balancing method to handle this resolution. NetScaler can be configured to interact with DNS in different ways:
	* Authoritative DNS (ADNS). NetScalers using ADNS mode are authoritative for a particular domain and all records on it.
	* DNS sub-delegation. Occurs when a DNS server (authoritative of the domain) delegates the responsibility of a sub-domain to a NetScaler system.
	* DNS proxy. When configured in this mode, NetScalers forward DNS requests to another server (external) handling the name resolution.
* **Method:** The method is an algorithm that the GSLB virtual server uses to select the best GSLB service from the topology. The algorithm assesses performance aspects that correspond to the actual selection criteria. The following methods are available:
  * Round Robin: Alternates incoming requests to be handled between the GSLB sites/services regardless of their load.
  * Round Trip Time (RTT): A measure of time or delay between the client’s local DNS server and the (GSLB) sites. NetScaler uses different mechanisms such as ICMP echo request/reply (PING), UDP, and TCP, to gather the RTT metrics.
  * Static Proximity: Uses an IP-address database to establish the proximity between the client’s local DNS server and the sites, then it uses this as criteria to make a selection.
  * Least Connections: Measures the least number of active connections on each site/service as selection criteria.
  * Least Response Time: Selects the site with the fewest active connections and the lowest average response time.
  * Least Bandwidth: Chooses the site that is currently managing the least amount of traffic (Mbps).
  * Least Packets: Selects the service that has received the least number of packets in the last 14 seconds.
  * Source IP address Hash: Makes a selection of the service based on the hashed value of the client IPv4 or IPv6 address.
  * Custom Load: Selects a service that is not handling any active transactions. If all of the services in the load balancing setup are handling active transactions, the appliance selects the service with the smallest load (CPU usage, memory, and response time).

* **MEP (Metric Exchange Protocol):** A proprietary protocol used to exchange metrics (load and network) and persistence information between sites. MEP provides health checking between the different sites/NetScalers in the GSLB mesh/topology. Using the criteria set by the administrator, MEP provides a way for sites to communicate and handle the traffic based on the selection parameters previously configured. MEP uses TCP ports 3009 and 3011. When MEP is disabled, the selection of methods is limited to the options listed before marked with an asterisk (*). Any other method chosen would revert back to Round Robin.
* **Monitoring:** The NetScaler engine periodically evaluates the state of the remote GSLB services by using either MEP or explicit monitors bound to the services in question. Monitors are used just like on a regular load balancing service. In the case of GSLB, adding monitors to local services is not required as this is typically controlled by MEP. 
* **Persistence:** An optional feature that establishes a site preference for a particular domain. In this particular use case, the traffic is not load balanced but handled by the same data center. This can be helpful in certain applications, like e-commerce, where transactional data is unique to each a site/server.
* **GSLB site:** Sites can be defined as datacenters or locations where a NetScaler system is configured/present. Each GSLB site is managed by a NetScaler system that is considered “local” to that site, while all other remote systems/sites are seen and treated as “remote” sites.
* **GSLB service:** It is an object that represents (and is bound to) a (regular) virtual server/VIP. It can be either local (same site) or remote.
* **GSLB virtual server:** A GSLB virtual server is assigned to one or more GSLB services that would typically be part of different (GSLB) sites. Traffic received on it gets load balanced between the sites bound to it. The site selection is done based on the method and use case.
* **GSLB domain:** It represents the domain or zone for which the GSLB virtual server is responsible. 
* **ADNS service:** A service represented by a combination of IP address and port, it is where DNS requests to a domain for which NetScaler is authoritative are sent. NetScaler takes those to the GSLB virtual server bound to that domain in order to get a response.