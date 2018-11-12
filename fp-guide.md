---

copyright:
  years: 2018
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# How to configure forward-proxy traffic redirection using the Citrix NetScaler VPX appliance
This guide provides you with a step-by-step configuration for a forward proxy setup using the Citrix NetScaler VPX appliance. This configuration was tested on a Citrix NetScaler VPX appliance running a software version of 11.1 (platinum feature edition) and 10Mbps performance.

<img src="images/fp1.png" alt="drawing" style="width: 600px;"/>

## What you'll accomplish

In this Step-by-Step guide you will learn how to configure the service:

Task  | Description
------------- | -------------
[Order the Citrix NetScaler VPX](order-vpx.html) | Begin by ordering a Citrix NetScaler VPX appliance.
[Request a Private Subnet](request-subnet.html) | Request a private subnet from IBM Support for your account.
[Enable Cache Redirection and Load Balancing capabilities](fp-cache.html) | Identify the your application's resources, such as origin pools and health check mechanisms.
[Configure the DNS Virtual Server](fp-dns.html) | Add your DNS resolvers, define your DNS service group, then define your DNS virtual server.
[Configure Cache Redirection for HTTP(S) traffic](fp-cache-http.html) | Configure the cache redirection for your forward proxy virtual server with HTTP or HTTPS traffic.
[Configure Cache Redirection for SSL traffic (Optional)](fp-cache-ssl.html) | Configure the cache redirection for your forward proxy virtual server with SSL traffic instead of HTTP or HTTPS.
[Configure Source NAT for Outbound Traffic](fp-nat.html) | Utilize your Citrix NetScaler VPX appliance to perform NAT on outbound traffic from your client machines.
[Update the Proxy Settings on the Client Machine’s Internet Browser (Optional)](fp-proxy-settings.html) | Update your proxy settings using your client machine's internet browser, if you desire.