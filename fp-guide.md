---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-21"

keywords:

subcollection: citrix-netscaler-vpx


---

{{site.data.keyword.attribute-definition-list}}

# Configuring forward-proxy traffic redirection by using the Citrix Netscaler VPX
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

You can configure a forward proxy setup by using the {{site.data.keyword.vpx_full}} appliance. This configuration was tested on a {{site.data.keyword.vpx_full}} appliance with software version 11.1 (platinum feature edition) and 10 Mbps performance.
{: shortdesc}

![Forward Proxy Traffic Redirection](images/fp1.png){: caption="Forward proxy traffic redirection" caption-side="bottom"}

## What to accomplish
{: #what-you-will-accomplish}

In this step-by-step guide, you can learn how to configure the service

| Task | Description |
| ---- | ----------- |
| [Order the {{site.data.keyword.vpx_full}}](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) | Begin by ordering a {{site.data.keyword.vpx_full}} appliance. |
| [Request a Private Subnet](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) | Request a private subnet from {{site.data.keyword.IBM}} Support for your account. |
| [Enable Cache Redirection and Load Balancing capabilities](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) | Identify your application's resources, such as origin pools and health check mechanisms. |
| [Configure the DNS Virtual Server](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) | Add your DNS resolvers, define your DNS service group, then define your DNS virtual server. |
| [Configure Cache Redirection for HTTP(S) traffic](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic) | Configure the cache redirection for your forward proxy virtual server with HTTP or HTTPS traffic. |
| [Configure Cache Redirection for SSL traffic](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) | Configure the cache redirection for your forward proxy virtual server with SSL traffic instead of HTTP or HTTPS. |
| [Configure Source NAT for Outbound Traffic](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) | Utilize your {{site.data.keyword.vpx_full}} appliance to perform NAT on outbound traffic from your client machines. |
| [Update the Proxy Settings on the Client Machine’s Internet Browser](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) | Update your proxy settings that use your client machine's internet browser, if you want. |
{: caption="Configuring the service" caption-side="top"}
