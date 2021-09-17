---

copyright:
  years: 2017
lastupdated: "2019-11-12"

keywords:

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

# Configure cache redirection for SSL traffic (optional)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

Instead of defining cache redirection for the virtual server with an HTTP or HTTPS protocol (as discussed in the [previous step](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic)) with your {{site.data.keyword.vpx_full}}, you may want to define it to handle SSL traffic.
{: shortdesc}

To do so, follow these steps:

1. Go to **Traffic Management > Cache Redirection > Virtual Servers** and click **Add**. Specify the name for your forward-proxy virtual server, select the SSL protocol and a cache type of **FORWARD**. Assign it an IP address from your private subnet, with its requisite port.

	![Virtual Server settings](images/fp14.png)

	Click **OK**.

2. Review the summary page and click **OK** to continue.
3. Specify your Redirect, DNS Virtual Server and Destination Virtual Server configurations.
4. Click **Certificate** under the **Advanced Settings** panel to view the SSL certificate related configuration.
5. Click the empty field **No Server Certificate**.
6. From the Select Server Certificate list menu, select your SSL server.
7. Enter the certificate configuration information as required.

	![Certificate configuration](images/fp15.png)

	Click **Install**.

8. Select **Bind**.

	![Bind](images/fp16.png)
