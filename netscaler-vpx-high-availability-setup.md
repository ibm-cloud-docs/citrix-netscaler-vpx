---
copyright:
  years: 2024
lastupdated: "2024-08-02"

keywords: ha, high availability, setup, configure, configuration

subcollection: citrix-netscaler-vpx
---

{{site.data.keyword.attribute-definition-list}}

# Setting up Citrix Netscaler VPX for High Availability (HA)
{: #setting-up-citrix-netscaler-vpx-for-high-availability-ha}
{: help}
{: support}

Load balancers are used to balance traffic over multiple application servers to improve performance and stability in a scalable application. Yet, a single load balancer is a single point of failure. Avoid this liability by configuring a High Availability (HA) {{site.data.keyword.vpx_full}} pair. Configuring an HA pair requires two Netscaler VPX servers. The secondary server steps in to continue load balancing if the primary fails.
{: shortdesc}

The SNIP (SubNet IP) is the IP seen by the load balanced servers as the source IP of the requests (connections) made to the VIP (Virtual IP) of the Netscaler VPX. Normally, in an HA pair setup, the SNIP does not change, but it is possible for it to do so during a failover event. When the two Netscalers are in the same subnet, it is possible for the SNIP of the secondary Netscaler VPX to change to the SNIP originally used by the primary Netscaler VPX. This situation does not cause any confusion for the servers that handle the request.

For an HA configuration, both NetScalers must be in the same VLAN and on the same subnet.

Make sure that you take the following prerequisite actions prior to configuration:

1. If you configure the pair active-active, any VIP subnets added to the instances must be of type "Routed to VLAN".
2. If you configure the pair active-passive, any VIP subnets added to the instances must either be "Routed to VLAN" or "Secondary routed to IP". They should also be routed to the public IP address of the primary node.

After ordering the two Netscaler VPX servers in the needed VLAN, and ordering the VIP and SNIP subnets to meet the prerequisites for your HA pair configuration, you can proceed:

1. Open two browser windows and log in to the advanced interface on both NetScalers. On the secondary NetScaler, go to **System > User Administration > Users** and set the root password to the same as the primary NetScaler. Then update the password on file in the IBM Cloud catalog on the device details page to match the password set for the secondary.

2. On the VPX you want to be secondary, click **System > High Availability**, then right click the first line and click **Edit**. Select **Stay Secondary** on the High Availability Status config drop-down box and click **OK**.

3. Select **Add**. Enter the system IP address of the other VPX (it is located in the High Availability tab on the primary), and enter the root login details. Leave the **Turn on INC** box cleared. Click **OK**.

   If you receive an error that the IPs are not in the same subnet, it is possible that both VPX servers are not in the same VLAN. Otherwise, you should now be able to open the primary server and select **Refresh** to see both servers in High Availability.

   The new NetScaler management IP for the secondary is one IP address lower than previously. If you cannot get any access to the secondary VPX, remove the high availability from the command line by using:

   `sh ha node`

   Then remove what would be the HA node:

   `rm ha node 1`

4. On the primary VPX you should see that the remote VPX is now syncing. Go to the secondary server and check the **Network > IPs** configuration. You should see the primary server's VIP and other IPs listed as passive.

5. Return to **System > High Availability** on the secondary server and click **Edit**. Select **ENABLED** in the drop-down box and press **OK**.

6. Force a failover to test. Refresh the screen and watch the IP addresses become active on the secondary. Failover again and watch them go passive. Ping the IPs to make sure that they work.

7. The primary server is now labeled primary and the secondary reports that it has a synchronization state of success.

Ensure that your local administrators know that the password in the Cloud console must be changed to be consistent anytime the passwords are changed on the local VPXs.  **Failing to do so causes HA Upgrades and license operations to fail, resulting in production outages.**  Your passwords must be consistent in three places: VPX device 1, VPX device 2, and the IBM Cloud console.
{: important}
