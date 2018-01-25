---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Set up Citrix Netscaler VPX as a Forwarding Proxy

A forwarding proxy acts as a single point of control between clients on an internal network and the Internet. A proxy allows the Network or Security Administrator the ability to create policies restricting access to Internet sites.

When a client on the internal network initiates a request, the IP address of the proxy will be used to initiate the request to the remote server on the Internet. The remote server in turn responds back to the proxy, which returns the response to the client.

Typically, a proxy is combined with a firewall to ensure the security of clients in an internal network.

## Step 1: Request VIPs to use in the Private Network 

When a Citrix NetScaler VPX load balancer is ordered from the {{site.data.keyword.BluSoftlayer_notm}} customer portal, it is assumed a reverse proxy is being requested. The requestor will be asked for the number of “public” IPs to be used as virtual IPs (VIPs).

In the case of a forward proxy, the VIPs need to be setup on the private network. A support ticket needs to be opened in order to request VIPs for the private network. The number of VIPs required will determine the size of the subnet requested in the ticket. The subnet information will be returned in the ticket.

In our example we requested a `/29` subnet, which resulted in the following:

* Created subnet `10.114.27.0/29` for use as private VIP's

* Subnet IP (SNIP) `10.114.52.101`, and routed subnet `10.114.27.0/29`

* VIPs `10.114.27.0-3` were added to the Citrix NetScaler VPX by the support team

## Step 2: Enable Load Balancing and Cache Redirect Features on the Citrix NetScaler VPX

By default, the load balancing and cache redirect features on the Citrix NetScaler VPX load balancer are disabled; the `enable ns feature cr lb` command enables them.


## Step 3: Create the Forward Proxy

Use the command line to issue the following commands on to the Citrix NetScaler VPX. In our scenario, only one of the two {{site.data.keyword.BluSoftlayer_notm}} DNS servers are added.  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

Line 1 creates the redirect cache. The protocol is HTTP and `10.114.27.3` is one of the VIPs requested on the private network. The port is default port 80 for HTTP, but since this address and port combination is going to be used as the proxy statement in the browser, the port can be changed to whatever is required.

Line 2 adds a load balancing VIP that will represent the “real” DNS.

Line 3 adds the IP address of the “real” DNS as a service. This address can be the customer DNS or routed back to the {{site.data.keyword.BluSoftlayer_notm}} supplied DNS resolvers.

Line 4 binds the VIP to the “real” server. All DNS requests to `10.114.27.4` will be sent to `10.0.80.12`.

Line 5 tells the forwarding proxy virtual server to use the virtual DNS for name resolution.

## Configuring the Client

Before continuing to customize the client to use the forwarding proxy, make sure that you cannot reach a public site (for example, http://www.ibm.com) by using the Firefox browser on the client. Since there should be no public interface on the client, this request should fail. 

The following example configures a Linux client.

A few changes need to be made to the client. The first change is to point the resolver on the client to the virtual DNS which can be done one of two ways.

You can manually edit the `/etc/resolv.conf` to point to the virtual address of the DNS. Be aware that client management tools may revert these changes back to the original settings.  

Or you can edit the `/etc/sysconfig/network-scripts/ifcfg-ethx` interface and add the `DNS1=` statement. Once set, the service network restart command can be issued to pick up the changes.

In either case, the DNS IP address will need to be configured as the virtual DNS address, and the client's browser will need to be configured to point requests to the Citrix NetScaler VPX forwarding proxy.

Use the following steps within Firefox to make the necessary changes:

1. Click **Preferences > Advanced > Network > Connection Settings**.

* Select **Manual Proxy Configuration** and enter the following:

  * **Address:** 10.114.27.3

  * **Port:** 80

  * Check the **Use this proxy server for all protocols** checkbox.

* Click **Save** and close the browser window.

The IP address `10.114.27.3` is the IP address of the forwarding cache created in Step 1.

At this point, the setup is complete and you can access the Internet from the resource isolated on the private network.

## Validating the Setup

Now that the client is configured to use the forwarding proxy, try an access a public site again. The request should now be successful.

The following display commands can be used to validate the state of the forwarding proxy.

**show cr policy:** Displays all existing cache redirection policies.

**show policy map:** Displays the map policies that have been configured and the related map policy information.

**show cr vserver:** Displays a specified cache redirection virtual server, or all configured cache redirection virtual servers.

**stat cr vserver:** Displays cache redirection vserver statistics.

Go to the [Citrix command reference guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.citrix.com/servlet/KbServlet/download/20679-102-665857/NS-CommandReference-Guide.pdf) for more documentation.

The configuration of a basic forwarding proxy on Citrix is fairly straightforward. It provides a way to give clients on an internal network a secure path to resources on the Internet. It also enables the Network Administrator to maintain a level of control over the network.

If implementing at a customer site, it is recommended to add a firewall to the configuration to further protect the resources.