---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-21"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Configure cache redirection for HTTP(S) traffic
{: #configure-cache-redirection-for-http-traffic}

You can configure cache redirection for HTTP or HTTPS traffic with your {{site.data.keyword.vpx_full}}.
{: shortdesc}

To do so, perform the following procedure:

1. Go to **Traffic Management > Cache Redirection > Virtual Servers** and click **Add**.
2. Specify the name of your forward-proxy virtual server. Select the **HTTP** protocol and the **Forward** cache type from their respective list menus. Then, assign an IP address to this virtual server from your private subnet.

    Click **OK** to continue.

3. Review the summary page and click **OK**.
4. Click **Traffic Settings** to view extra configuration settings.
5. From Traffic Settings select one of the following three redirect options, depending on your requirements:
   * **Cache** - Directs all outbound requests to your local cache server pool.
   * **Policy** - Checks the cache redirection policy to determine whether the request forwards to the cache server pool or to the destination servers (origin).
   * **Origin** – Directs all outbound requests to the respective destination servers (origin).

6. From the list **DNS Virtual Server Name**, select the previously-configured DNS virtual server, and set the **Redirect** option to **Origin**.

    The **Destination Virtual Server** setting is used when outbound traffic is to be directed to the local cache server pool. Leave it empty when you want to direct all your outbound traffic to origin servers.
    {: note}

7. Click **OK** followed by **Done**.
