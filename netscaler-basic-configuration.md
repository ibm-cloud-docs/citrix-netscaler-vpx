---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: basics, configure, configuration, gui, pool

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Basic Load Balancing Configuration
{: #basic-load-balancing-configuration}

Consider a company that has a basic social community website where end-users can register for an account that requires no sensitive information, after which the user can log in and post pictures of their pets. There are three web/application servers, and one database server to back them up. The domain and DNS are hosted with {{site.data.keyword.BluSoftlayer_notm}}, and because they have a small environment, the NetScaler and web/app servers are all in the same VLAN. This simplifies things, as no further configuration is needed for the NetScaler to set up a basic load balancing policy. The following procedure is an oversimplified explanation of the traffic flow in this instance:

1. A user enters the URL into their browser.
2. The URL's DNS record points to one of the Public VIPs on the NetScaler.
3. The NetScaler receives the traffic on that VIP, and makes note of the traffic's protocol being used (HTTP port 80 traffic).
4. The NetScaler then passes that traffic to one of the servers in the server pool, based on the balancing method defined (round robin, persistence IP, and so on).
5. The server then accepts the traffic and the user connects and logs in.

In order to accomplish this, the NetScaler would need to be configured to handle this traffic. Since the VIP, the DNS server's IP, and the SNIP are already configured, this simplifies the configuration.

In the NetScaler GUI, on the Configuration screen, expand **Traffic Management** on the left-hand side. Expand the subsection titled **Load Balancing**. Then tell the NetScaler what target servers will be included in the load balancing policy, by following this procedure:

1. Under Load Balancing, click on **Servers**.
2. Click **Add**.
3. Enter the Server Name of the server (for example, Web1).
4. Enter the IP address of the server.
5. Leave the **Traffic Domain** field blank, as you are only concerned with using the default traffic domain in this scenario.
6. Enter any comments you would like about this server.
7. Click **Create**.

Repeat this procedure for all servers in the pool.  

**TIP:** To keep servers easily identifiable, use a similar naming convention for servers within the same pool (for example, Web1, Web2, Web3, and so on).

Next, create your Services. You will be creating a Service for each Server that you just entered. The Service is what configures the connection between the NetScaler and the servers in the pool. Each service has a name and specifies an IP address, a port, and the type of data that is served.

1. Click **Traffic Management > Load Balancing > Services**.
2. Click **Add**.
3. Create a service for each server you created earlier, utilizing the same information.

Next, create a Virtual Server. The Virtual Server is a sort of virtual connection between the VIP used for the load balanced servers and services you created earlier.

1. Click **Traffic Management > Load Balancing > Virtual Servers**.
2. Click **Add**.
3. Name the Virtual Server.
4. Designate the Protocol that you will be balancing (HTTP).
5. Leave the IP Address Type as the default (IP Address). The IP address field is where you will enter the VIP that you will be using as the entry point for all of your users.
6. Designate the port. The default is port 80.
7. Click **OK**.

Now, bind the services you created to your Virtual Server.

1. On the Virtual Servers screen, click the **No Load Balancing Virtual Server Service Binding** link.
2. Bind each of the previously created Services to the Virtual Server.
3. Click **Done**.
4. Click the **Refresh** button. The State and Effective State will show as green.

You have created a load balancing pool and policy for your website.

**NOTE:** To learn more about configuration of the Citrix NetScaler VPX device, please visit the [Citrix documentation page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.citrix.com/en-us/netscaler.html). For further assistance, contact the {{site.data.keyword.BluSoftlayer_notm}} support and sales.
