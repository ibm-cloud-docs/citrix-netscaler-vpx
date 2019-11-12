---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: proxy, update

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

# Update the Proxy Settings on the Client Machine’s Internet Browser (Optional)
{: #update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-}

To update your proxy settings using your client machine's internet browser, perform the following steps:

1. Go to **Internet Options** in your browser settings and configure it to use a proxy server for outgoing requests.
2. Use the IP address of your cache redirection virtual server that was defined in previous steps as your proxy.

These proxy settings may not be necessary if the {{site.data.keyword.vpx_full}} appliance is in the direct layer-3 path between client machines and the internet.
{: note}

![Proxy settings](images/fp17.png)
