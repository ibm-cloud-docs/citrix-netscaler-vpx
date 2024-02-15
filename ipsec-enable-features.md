---

copyright:
  years: 2019
lastupdated: "2019-11-13"

keywords:

subcollection: citrix-netscaler-vpx


---

{{site.data.keyword.attribute-definition-list}}

# Enabling the features in Citrix Netscaler VPX
{: #enable-required-features-in-vpx}

You can enable the features in {{site.data.keyword.vpx_full}} to create the IPsec VPN.
{: shortdesc}

To do so, perform the following procedure:

1.	Access the VPX GUI (graphical user interface).
2.	Browse to **System > Settings > Configure Modes** and enable **Layer 3 Mode (IP Forwarding)**.
3.	Go to **System > Settings > Configure Advanced Features** and enable **Cloud Bridge**.

To enable these features in the CLI, run the following commands:

```sh
> enable ns feature CloudBridge
> enable ns mode L3

```

See [Managing your Citrix Netscaler VPX](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler) for extra instructions on connecting to the NetScaler with the GUI or SSH.
