---

copyright:
  years: 2019
lastupdated: "2019-11-13"

keywords: ipsec, vpn, tunnel

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank_"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Enabling the required features in Citrix Netscaler VPX
{: #enable-required-features-in-vpx}

You can enable the required features in {{site.data.keyword.vpx_full}} to create the IPsec VPN.
{: shortdesc}

To do so, perform the following procedure:

1.	Access the VPX GUI (Graphical User Interface).
2.	Navigate to **System > Settings > Configure Modes** and enable **Layer 3 Mode (IP Forwarding)**.
3.	Go to **System > Settings > Configure Advanced Features** and enable **Cloud Bridge**.

To enable these features in the CLI, execute the following commands:

```
> enable ns feature CloudBridge
> enable ns mode L3

```

For additional instructions on connecting to the NetScaler using the GUI or SSH, visit the [following article](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler)
