---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-21"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Configure source NAT for outbound traffic
{: #configure-source-nat-for-outbound-traffic}

Network address translation (NAT) remaps one IP address space into another. This procedure is done by modifying network address information in the IP header of packets while they are in transit across a traffic routing device.
{: shortdesc}

You can utilize your {{site.data.keyword.vpx_full}} appliance to perform NAT on outbound traffic from your client machines. To do so:

1. Go to **System > Network > Routes**, and navigate to the **RNAT** tab. Click **Configure RNAT**.

2. Specify the source subnet (and mask) to which you want to apply RNAT and click **OK**.

The Internet-bound traffic that is sourced from any IP in this subnet now uses NAT for traffic on the Citrix NetScaler’s public IP address.
