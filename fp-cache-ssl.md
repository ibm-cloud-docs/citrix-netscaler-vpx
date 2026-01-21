---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-21"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Configure cache redirection for SSL traffic
{: #configure-cache-redirection-for-ssl-traffic-optional-}

Instead of defining cache redirection for the virtual server with an HTTP or HTTPS protocol (discussed [previously](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic)), you can also define it to handle SSL traffic.
{: shortdesc}

To do so, follow these steps:

1. Go to **Traffic Management > Cache redirection > Virtual servers** and click **Add**. Enter the name for your forward-proxy virtual server. Then, select the SSL protocol and a cache type of **FORWARD**. Assign it an IP address from your private subnet, with its requisite port.

   Click **OK**.

2. Review the summary page and click **OK** to continue.
3. Specify your Redirect, DNS Virtual Server, and Destination Virtual Server configurations.
4. Click **Certificate** under the **Advanced Settings** panel to view the SSL certificate-related configuration.
5. Click the empty field **No Server Certificate**.
6. From the Select Server Certificate list menu, select your SSL server.
7. Enter the certificate configuration information as required.

   Click **Install**.

8. Select **Bind**.
