---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-12"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Configure the DNS virtual server
{: #configure-the-dns-virtual-server}

To further define forward proxy traffic redirection by using the {{site.data.keyword.vpx_full}}, configure a DNS virtual server:
{: shortdesc}

1. Go to Traffic **Management > Load Balancing > Servers**.
2. Click **Add** to add the two {{site.data.keyword.cloud}} DNS resolvers - `10.0.80.11` and `10.0.80.12`.
3. Create and define your DNS Service Group by going to **Traffic Management > Load Balancing > Service Groups** and selecting **Add**.
4. Select the DNS protocol, then click **OK**.
5. On the next screen, add the new DNS resolvers as member servers to this DNS service group by first clicking the empty field under **Service Group Members**.
6. From the **Create Service Group Member** panel, specify DNS port `53`, then click **Create**.
7. Click **Close** then click **Done**.

    Assuming the two IBM Cloud DNS resolvers can be reached from your {{site.data.keyword.vpx_full}} appliance, the service group shows as green.

8. Now, go to **Traffic Management > Load Balancing > Virtual Servers** and click **Add** to define your DNS Virtual server.
9. In the Basic Settings section, give a name to your virtual server. Then choose the DNS protocol and port `53`, then assign an IP address from your private subnet.
10. On the following page, click on the empty field that is labeled **No Load Balancing virtual Server ServiceGroup Binding**.
11. Select your previously-defined DNS service group from the list menu and click **Bind**.  
12. Click **Continue** followed by **Done**.

Your DNS virtual server state now shows as green.
