---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"

keywords: faq, faqs, questions, vpx, options, ipv6, traffic, network, ha, ssl, vpn

subcollection: citrix-netscaler-vpx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.vpx_full}} 的常见问题
{: #faqs-for-citrix-netscaler-vpx}

下面是使用 {{site.data.keyword.vpx_full}} 时会遇到的常见问题。

## 什么是 {{site.data.keyword.vpx_full}}？
{: faq}

Citrix NetScaler 是一种应用程序交付控制器，通过加速性能，确保应用程序可用性和保护并大幅降低运营成本，从而使应用程序的提升程度达到原来的 5 倍。选择满足应用程序需求的最佳 Citrix NetScaler 版本，并将其部署在适合您的性能需求的专用系统上。要了解有关 Citrix NetScaler 的更多信息，请参阅 Citrix Web 站点上的 [NetScaler 页面 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){:new_window}。

## 为什么需要负载均衡？
{: faq}

流量负载均衡会在多个服务器上分布应用程序请求和负载，因此已成为诸多客户实现的关键方面。此外，它还给总体拓扑带来了一些优点，包括：

* 安全性。将基于 IP 协议和端口号创建应用程序服务器的逻辑隔离或拒绝流量请求。
* 高可用性。内容将复制到池或服务器组，以保证对主机可用。
* 可扩展性。随着需求的增加，可以添加额外的服务器，从而使负载均衡器能够将工作负载分布到额外的服务器上。
* 效率。配置负载均衡后，会动态分布工作负载。例如，可以更高效地使用 CPU 等资源。

## {{site.data.keyword.BluSoftlayer_notm}} 中提供了多少负载均衡选项？
{: faq}

有关 IBM© 负载均衡器产品的详细比较，请参阅[探索 Load Balancer](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)。

## NetScaler 支持 IPv6 吗？
{: faq}

支持。{{site.data.keyword.BluSoftlayer_notm}} 公用网络上同时支持 IPv6 和 IPv4。

## NetScaler 会对专用网络上的流量进行负载均衡吗？
{: faq}

会的，NetScaler 是扩展到专用网络的唯一 {{site.data.keyword.BluSoftlayer_notm}} 负载均衡产品。

## 可以将 NetScaler 配置为报告客户机的源 IP 地址，而不报告 NetScaler 设备的源 IP 吗？
{: faq}

可以，在 NetScaler 的“高级管理界面”中，可以将**使用源 IP (USIP)** 参数设置为**是**，以允许报告客户机的源 IP 而不报告 NetScaler 的源 IP。

通过在设备上启用 USIP 地址方式，可使设备在与服务器进行通信时，更灵活地使用 IP 头中提供的客户机 IP 地址。通过启用此方式，设备将打开与客户机 IP 地址的服务器连接，并在连接复用中将客户机 IP 地址纳入考虑中。因此，此方式有利于根据客户机 IP 地址对每个客户机进行有限复用。

## 用于在 HA 配置中的节点之间交换 HA 相关信息的各种端口是什么？
{: faq}

端口 3010，用于同步和命令传播。UDP 端口 3003，用于交换脉动信号包。

## 哪个版本的 NetScaler VPX 包含全局服务器负载均衡 (GSLB)？
{: faq}

Platinum。

## 可以在 HA 配置中使用 NetScaler 吗？
{: faq}

可以，NetScaler VPX 设备支持高可用性 (HA) 配置。

除非以 HA 方式配置使用合作伙伴，否则 NetScaler VPX 服务器无冗余。作为备份和恢复策略的一部分，强烈建议在使用 NetScaler VPX 时部署 HA 环境。

为其他硬件和软件组件提供冗余也很重要。例如，电源和本地磁盘驱动器可能没有冗余。这些组件中的故障可能会导致数据丢失。

## {{site.data.keyword.BluSoftlayer_notm}} NetScaler 产品包含 SSL VPN 功能吗？
{: faq}

包含，此功能称为 NetScaler Gateway™，并且所有版本中都包含此功能。有关此功能的更多信息，请访问 [Citrix Web 站点 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.citrix.com/products/netscaler-adc/){: new_window}
