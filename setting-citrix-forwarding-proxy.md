---
copyright:
  years: 2024
lastupdated: "2024-08-02"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Setting up Citrix Netscaler VPX as a forwarding proxy
{: #setting-up-citrix-netscaler-vpx-as-a-forwarding-proxy}

You can set up your {{site.data.keyword.vpx_full}} as a forwarding proxy. A forwarding proxy acts as a single point of control between clients on an internal network and the internet. A proxy allows the Network or Security Administrator the ability to create policies that restrict access to internet sites.
{: shortdesc}

When a client on the internal network initiates a request, the IP address of the proxy is used to initiate the request to the remote server on the internet. The remote server in turn responds to the proxy, which returns the response to the client.

Typically, a proxy is combined with a firewall to ensure the security of clients in an internal network.

## Step 1: Request VIPs to use in the private network
{: #step-1-request-vips-to-use-in-the-private-network}

When a {{site.data.keyword.vpx_full}} load balancer is ordered from the IBM Cloud catalog, it is assumed a reverse proxy is being requested. The requester is asked for the number of “public” IPs to be used as virtual IPs (VIPs).

If a forward proxy exists, the VIPs need to be setup on the private network. Request VIPs for the private network by using an IBM Support case. The number of VIPs you need determine the size of the subnet that is requested in the Support case. The subnet information is returned in the Support case.

In this example, you request a `/29` subnet, which results in the following:

* Created subnet `10.114.27.0/29` for use as private VIPs
* Subnet IP (SNIP) `10.114.52.101`, and routed subnet `10.114.27.0/29`
* The support team added VIPs `10.114.27.0-3` to the {{site.data.keyword.vpx_full}}

## Step 2: Enable load balancing and cache redirect features on the {{site.data.keyword.vpx_full}}
{: #step-2-enable-load-balancing-and-cache-redirect-features-on-the-citrix-netscaler-vpx}

By default, the load balancing and cache redirect features on the {{site.data.keyword.vpx_full}} load balancer are disabled; the `enable ns feature cr lb` command enables them.


## Step 3: Create the forward proxy
{: #step-3-create-the-forward-proxy}

Use the command line to issue the following commands on to the {{site.data.keyword.vpx_full}}. In this scenario, only one of the two IBM Cloud DNS servers are added.  

```sh
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```
{: codeblock}

Line 1 creates the redirect cache. The protocol is HTTP and `10.114.27.3` is one of the VIPs requested on the private network. The default port is 80 for HTTP, but because this address and port combination is the proxy statement in the browser, the port can be changed.

Line 2 adds a load balancing VIP that represents the “real” DNS.

Line 3 adds the IP address of the “real” DNS as a service. This address can be the customer DNS or routed back to the IBM Cloud supplied DNS resolvers.

Line 4 binds the VIP to the “real” server. All DNS requests to `10.114.27.4` are sent to `10.0.80.12`.

Line 5 tells the forwarding proxy virtual server to use the virtual DNS for name resolution.

## Configuring the client
{: #configuring-the-client}

Make sure you customize the client to use the forwarding proxy, make sure that you cannot reach a public site (for example, `http://www.ibm.com`) by using the Firefox browser on the client. Because no public interface exists on the client, this request should fail.

The following example configures a Linux client.

You need to make a few changes to the client, the first of which is to point the resolver on the client to the virtual DNS. This process is done in one of two ways.

You can manually edit the `/etc/resolv.conf` to point to the virtual address of the DNS. Client management tools can revert these changes back to the original settings.  

Or you can edit the `/etc/sysconfig/network-scripts/ifcfg-ethx` interface and add the `DNS1=` statement. After this configuration is set, issue the service network restart command to pick up the changes.

In either case, the DNS IP address must be configured as the virtual DNS address, and the client's browser that is configured to point requests to the {{site.data.keyword.vpx_full}} forwarding proxy.

Use the following steps within Firefox to make the necessary changes:

1. Click **Preferences > Advanced > Network > Connection Settings**.
1. Select **Manual Proxy Configuration** and enter the following:
    * **Address:** 10.114.27.3
    * **Port:** 80
    * Check the **Use this proxy server for all protocols** checkbox.
1. Click **Save** and close the browser window.

The IP address `10.114.27.3` is the IP address of the forwarding cache that is created in Step 1.

The setup is complete and you can access the internet from the resource that is isolated on the private network.

## Validating the setup
{: #validating-the-setup}

Now that the client is configured to use the forwarding proxy, try to access a public site again. The request should now succeed.

The following display commands can be used to validate the state of the forwarding proxy.

* **show cr policy:** Displays all existing cache redirection policies.
* **show policy map:** Displays the map policies that are configured and the related map policy information.
* **show cr vserver:** Displays a specified cache redirection virtual server, or all configured cache redirection virtual servers.
* **stat cr vserver:** Displays cache redirection Vserver statistics.

Configuring a basic forwarding proxy on Citrix provides a way to give clients on an internal network a secure path to resources on the internet. It also enables the Network Administrator to maintain a level of control over the network.

For customer site implementations, add a firewall to the configuration to further protect the resources.
