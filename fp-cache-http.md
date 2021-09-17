---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-13"

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

# Configure cache redirection for HTTP(S) traffic
{: #configure-cache-redirection-for-http-traffic}

You can configure cache redirection for HTTP or HTTPS traffic with your {{site.data.keyword.vpx_full}}.
{: shortdesc}

To do so, follow these steps:

1. Go to **Traffic Management > Cache Redirection > Virtual Servers** and click **Add**.
2. Specify the name of your forward-proxy virtual server. Select the **HTTP** protocol and the **Forward** cache type from their respective list menus. Then assign an IP address to this virtual server from your private subnet.

    ![Virtual Server setup](images/fp12.png)

    Click **OK** to continue.

3. Review the summary page and click **OK**.  
4. Click **Traffic Settings** to view additional configuration settings.
5. From Traffic Settings select one of the following three redirect options, depending on your requirements:
   * **Cache** - Directs all outbound requests to your local cache server pool.
   * **Policy** - Checks the cache redirection policy to determine if the request should be forwarded to the cache server pool or to the destination servers (origin).
   * **Origin** – Directs all outbound requests to the respective destination servers (origin).

6. From the list **DNS Virtual Server Name**, select the previously-configured DNS virtual server, and set the **Redirect** option to **Origin**.

    ![Redirect selection](images/fp13.png)

    The **Destination Virtual Server** setting is used when outbound traffic is to be directed to the local cache server pool. Leave it empty when you want to direct all your outbound traffic to origin servers.
    {: note}

7. Click **OK** followed by **Done**.
