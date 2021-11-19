---

copyright:
  years: 1994, 2019
lastupdated: "2019-11-12"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Basic load balancing configuration
{: #basic-load-balancing-configuration}

Consider a company that has a basic social community website where end-users can register for an account that requires no sensitive information, after which the user can log in and post pictures of their pets. There are three web/application servers, and one database server to back them up. The domain and DNS are hosted with IBM Cloud, and because they have a small environment, the NetScaler and web/app servers are all in the same VLAN. This simplifies things, because no further configuration is needed for the NetScaler to set up a basic load balancing policy.
{: shortdesc}

The following procedure is an oversimplified explanation of the traffic flow in this instance:

1. A user enters the URL into their browser.
2. The URL's DNS record points to one of the public VIPs on the NetScaler.
3. The NetScaler receives the traffic on that VIP, and makes note of the traffic's protocol being used (HTTP port 80 traffic).
4. The NetScaler then passes that traffic to one of the servers in the server pool, based on the balancing method defined (round robin, persistence IP, and so on).
5. The server then accepts the traffic and the user connects and logs in.

In order to accomplish this, the NetScaler needs to be configured to handle this traffic. Because the VIP, the DNS server's IP, and the SNIP are already configured, this simplifies the configuration.

## Creating servers
{: #create-basic-servers}

In the NetScaler GUI, on the Configuration screen, expand **Traffic Management** on the left-hand side. Expand the subsection titled **Load Balancing**. Then tell the NetScaler what target servers to include in the load balancing policy, by following this procedure:

1. In Load Balancing, click **Servers**.
2. Click **Add**.
3. Enter the name of the server (for example, Web1).
4. Enter the IP address of the server.
5. Leave the **Traffic Domain** field blank, because you are only concerned with using the default traffic domain in this scenario.
6. Enter any comments you want about this server.
7. Click **Create**.

Repeat this procedure for all servers in the pool.  

To keep servers easily identifiable, use a similar naming convention for servers within the same pool (for example, Web1, Web2, Web3, and so on).
{: tip}


## Creating services
{: #create-basic-services}

Next, create your services. You will be creating a service for each server that you just entered. The service is what configures the connection between the NetScaler and the servers in the pool. Each service has a name and specifies an IP address, a port, and the type of data that is served.

1. Click **Traffic Management > Load Balancing > Services**.
2. Click **Add**.
3. Create a service for each server you created earlier, utilizing the same information.

Next, create a virtual server. The virtual server is a sort of virtual connection between the VIP used for the load-balanced servers and services you created earlier.

1. Click **Traffic Management > Load Balancing > Virtual Servers**.
2. Click **Add**.
3. Name the virtual server.
4. Designate the protocol that you are balancing (HTTP).
5. Leave the IP address type as the default (IP Address). The IP address field is where you enter the VIP that you are using as the entry point for all of your users.
6. Designate the port. The default is port 80.
7. Click **OK**.

## Binding services
{: #binf-basic-services}

Now, bind the services you created to your virtual server.

1. On the Virtual Servers screen, click the **No Load Balancing Virtual Server Service Binding** link.
2. Bind each of the previously created services to the virtual server.
3. Click **Done**.
4. Click the **Refresh** button. The State and Effective State show as green.

You have created a load balancing pool and policy for your website.

To learn more about configuration of the {{site.data.keyword.vpx_full}} device, see the [Citrix documentation page](https://docs.citrix.com/en-us/netscaler.html){: external}. For further assistance, contact the IBM Cloud Support and sales.
{: note}
