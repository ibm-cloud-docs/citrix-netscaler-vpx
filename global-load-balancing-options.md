---
copyright:
  years: 1994, 2017
lastupdated: "2019-11-12"

keywords: gslb, vpx, cdn, object storage

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Global load balancing
{: #global-load-balancing}

Global server load balancing (GSLB) is a method to split traffic across multiple servers using DNS and geographical locations as the means to determine where server traffic should be sent. Generally, a global load balancer sends a client request to a server that is closer to the client, decreasing latency and improving performance.
{: shortdesc}

You may not require a full implementation of a global load balancing solution. GSLB requires multiple instances of a suitable device that can perform this function, and depending on your needs, other solutions might be more attractive to you. If you need entire websites and applications, then GSLB is a good choice. If you only need portions of your content, such as images, videos, or other large files, then a [Content Delivery Network](/docs/CDN?topic=CDN-about-content-delivery-networks-cdn-) might be more suitable (and easier to deploy).

## {{site.data.keyword.vpx_full}}
{: #citrix-netscaler-vpx}

The {{site.data.keyword.vpx_full}} is the only customer configurable device that does true global load balancing. NetScaler is a multi-function appliance that can perform DNS based global load balancing lookups. You can point to the NetScaler as a DNS server, and the device will look over the servers it is configured to load balance for, perform a distance calculation, and return a record with the IP of the server closest to the client request.

For global load balancing, you would have a NetScaler appliance configuration in each data center. Each NetScaler appliance configuration may be a single Netscaler or a pair of Netscalers in an HA pair, depending on your requirements, providing local load balancing services for the servers behind them. The devices are configured to talk to one another so they exchange state information on each server assigned to global load balancer rotation. Any DNS request that comes to these configured NetScalers can return a proper record for a server that is online and responsive. Any server not responsive is removed from the rotation and another selected.

You must already have load balancing set up, even if it is only one server being balanced. You will need additional IP addresses for some services, namely the GSLB site IP. This IP is used by the NetScaler to communicate with the other NetScalers in the global load balancing protocol.

The following global balancing procedure uses:

### VPX1
{: #vpx1}

`50.97.235.236` is named `VPX1Vserver`, and is the local load balancing VIP for that device. `50.23.66.52` will be called `VPX1site`, and is the local IP for that device's GSLB.

### VPX2
{: #vpx2}
`208.43.241.249` is used for `VPX2Vserver`, and the GSLB IP is `208.43.224.4`, called `VPX2site`.

1. Go to **Traffic Management > GSLB** and right click to enable the feature. Then, select **Sites** and **Add**.

2. On the first device, enter the Name as VPX1, the Type as local, and the IP as `50.23.66.52`, then select **Close**.

	You should see the site listed with a status of green. Do not add a remote site yet.

3. Go to **Traffic Management > GSLB** and select the **GSLB Wizard**. Click **Next**. Enter the hostname that you will be load balancing (in this example, `gslb.tsstesting.com`) Leave the Record Type as A, and the Service Type ANY. The virtual server name will populate itself. Click **Next**.

4. Choose your form of balancing and persistence method just like you would with regular load balancing. Click **Next**.

5. The site is already populated, so you don't have to add anything. Instead, click on the green '+' next to the first site's name. Select the Vserver on that device from the list and click **Create**. You should see that the site is configured with the site IP and the Vserver IP of your load balanced setup, and that it is green. Click **Next**, **Finish**, and **Exit**.

6. Perform the same actions on the next NetScaler, using the values for that server.

7. On both servers, go to **Traffic Management > DNS > Records > A records**, and examine the list. You should see `root.servers.net` entries, as well as your hostname, with a type of `GSLB DOMAIN`.

8. Go to **Traffic Management > DNS > Name Servers** and click **Add**. Enter an IP address on the NetScaler (such as, the public IP of the device). Click **Local** and leave the protocol as UDP. Click **Create** then **Close**. You should see the effective state as enabled and up.

9. Go to **System > Network > IPs** and open the GSLB IP address. Make sure that **Management** is selected for both machines.

10. Next, on both servers, go back to **Traffic Management > GSLB** and go through the wizard again. This time, click **Next**, and select **Modify Configuration for Existing Domains**. Select the hostname from the list and then click **Next** twice.

11. In the site address field, put in the site IP address of the other NetScaler and give it the other NetScaler's site name and click **Add**. The site will be populated with an option to click the green '+' again. Click the remote site plus sign to add another site. Enter the Vserver service IP (the one for the load balanced servers, not the GSLB site IP) and the port, click **Create** and **Close**, **Next**, **Finish** then **Exit**.

If everything has been working up to this point, and both servers are configured, everything should have a status of green in the GSLB Virtual Servers, Services and Sites. You will notice that there are now two entries in GSLB services on both machines if they are properly synchronized. At this point, the servers are now communicating with each other.

You now have to configure DNS.

In our example, `gslb.tsstesting.com`, you would create NS and glue records in the tsstesting.com zone:

  ```
    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; nameserver IP of first NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; nameserver IP of second NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias to the GSLB object on the NetScaler appliance
    ```

Remember, you can only use CNAMEs with hostnames, not the root of the domain.

This configuration sets the name servers for requests for `gslb.tsstesting.com` to the NetScaler IPs you configured DNS on. The CNAME record translates `tsstesting.com` to a request for `gslb.tsstesting.com`. Any requests for `www.tsstesting.com` will then go to the NetScaler to be resolved, and will return a record based on the load balancing method you configured.

For more information on NetScaler global load balancing, refer to:
* [Configuring the Netscaler for global load balancing ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://support.citrix.com/article/CTX110348){: new_window}
* [How DNS(Domain Name System) works with GSLB feature on NetScaler ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.citrix.com/article/CTX122619){: new_window}
* [Information on the MEP protocol and site monitoring ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://support.citrix.com/article/CTX111081){: new_window}

There are other products that can offer a similar functionality for spreading out traffic on a geographical basis:

### CDN
{: #cdn}

Content delivery networks (CDN) allow you to upload or provide an origin server to geographically dispersed cache servers, which then provide the content to the requesting client. CDNs work best with static, bulk content, such as images and videos that does not change over time.

For more details on CDN, refer to [this documentation](/docs/CDN?topic=CDN-getting-started).

### Object storage
{: #object-storage}

IBM Cloud's Object Storage can be configured to use multiple geographic locations in various data centers to provide content. A geographically aware application can perform location lookups on the client request and return a URL to Object Storage that is close to the client. Object Storage also comes with a CDN front end, if needed, to provide additional caching services as noted above.

For more information and an introduction to Object Storage, refer to [this documentation](/docs/cloud-object-storage?topic=cloud-object-storage-about).
