---

copyright:
  years: 2018
lastupdated: "2018-09-20"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Add and Configure the SSL Virtual Server
To add and configure your SSL Virtual Server, perform the following procedure:

1. Navigate to **System > Settings > Configure Basic Features**. Select **SSL Offloading** then click **OK**.
2. In the NetScaler GUI, navigate to **Traffic Management > Load Balancing > Services > Add**, and specify the name, the IP address, and set the protocol as **HTTP**. Hit **OK** to finish.
3. Confirm the service is operational:

	<img src="images/15-confirm-service.png" alt="drawing" style="width: 700px;"/>

4. Repeat step two for any additional servers.
5. Navigate to **Traffic Management > Load Balancing > Virtual Servers >** and click **Add**. Specify the name and selet **SSL** as the Protocol, then enter the public IP Address. Hit **OK** to finish.
6. Now select **No Load Balancing Virtual Server Service Binding** and click **Select**. Select the service(s) you created in the previous steps and click Select, then click **Bind/Continue**.

	<img src="images/18-bind-service.png" alt="drawing" style="width: 700px;"/>

7. Finally, click **No Server Certificate**, then click **Select Server Certificate** and select the certificate you installed earlier. Click **Select**, then **Bind/Continue**, then **DONE** to finish.