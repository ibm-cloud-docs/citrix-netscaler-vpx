---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-23"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Add and configure the SSL virtual server
{: #add-and-configure-the-ssl-virtual-server}

You can add and configure your SSL Virtual Server for use with the Hardware Security Monitor (HSM) of your {{site.data.keyword.vpx_full}}.
{: shortdesc}

To do so, perform the following procedure:

1. Browse to **System > Settings > Configure Basic Features**. Select **SSL offloading** then click **OK**.
2. In the NetScaler GUI, navigate to **Traffic Management > Load Balancing > Services > Add**, and specify the name, the IP address, and set the protocol as **HTTP**. Select **OK** to finish.
3. Confirm that the service is operational:
4. Repeat step two for any additional servers.
5. Navigate to **Traffic Management > Load Balancing > Virtual Servers >** and click **Add**. Specify the name and select **SSL** as the Protocol. Then, enter the public IP address. Select **OK** to finish.
6. Now, select **No Load Balancing Virtual Server Service Binding** and click **Select**. Select the services that you created in the previous steps and click **Select**, then click **Bind/Continue**.
7. Finally, click **No Server Certificate**, then click **Select Server Certificate** and select the certificate that you installed earlier. Click **Select**, then **Bind/Continue**, then **DONE** to finish.
