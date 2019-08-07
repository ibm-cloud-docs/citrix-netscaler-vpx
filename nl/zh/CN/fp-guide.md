---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: proxy, traffic, appliance

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 使用 {{site.data.keyword.vpx_full}} 设备配置正向代理流量重定向
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

本指南为您提供了使用 {{site.data.keyword.vpx_full}} 设备时设置正向代理的逐步配置。此配置已在运行软件版本 11.1（Platinum 功能版本）和 10 Mbps 性能的 {{site.data.keyword.vpx_full}} 设备上进行过测试。

<img src="images/fp1.png" alt="图样" style="width: 600px;"/>

## 需要完成的任务
{: #what-you-ll-accomplish}

在此逐步指南中，您将了解如何配置服务：

任务|描述
------------- | -------------
[订购 {{site.data.keyword.vpx_full}}](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance)|首先订购 {{site.data.keyword.vpx_full}} 设备。
[请求专用子网](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet)|向 IBM© 支持人员为您的帐户请求专用子网。
[启用高速缓存重定向和负载均衡功能](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities)|识别应用程序的资源，例如源池和运行状况检查机制。
[配置 DNS 虚拟服务器](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server)|添加 DNS 解析器，定义 DNS 服务组，然后定义 DNS 虚拟服务器。
[为 HTTP(S) 流量配置高速缓存重定向](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic)|为具有 HTTP 或 HTTPS 流量的正向代理虚拟服务器配置高速缓存重定向。
[为 SSL 流量配置高速缓存重定向（可选）](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-)|为具有 SSL 流量（而不是 HTTP 或 HTTPS 流量）的正向代理虚拟服务器配置高速缓存重定向。
[为出站流量配置源 NAT](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic)|利用 {{site.data.keyword.vpx_full}} 设备从客户端机器对出站流量执行 NAT。
[在客户端机器的因特网浏览器上更新代理设置（可选）](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-)|使用客户端机器的因特网浏览器更新代理设置（如果需要）。
