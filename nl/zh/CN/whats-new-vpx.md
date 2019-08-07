---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: updates, additions, version

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.vpx_full}} 的最近更新
{: #recent-updates-for-citrix-netscaler-vpx}

## V12.1
{: #version-12-1}

### 具有多个 IP 地址的虚拟服务器
{: #virtual-servers-with-multiple-ip-addresses}
现在，您可以使用多个非连续/连续 VIP IPv4 和 IPv6 地址来创建单个负载均衡虚拟服务器。每个与虚拟服务器绑定的 VIP 地址都将被视为单个虚拟服务器。

有关此功能的更多信息，请参阅此 Citrix 文章 [Multiple IP virtual servers ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}。

### SSL
{: #ssl}
已对 SSL 连接应用了以下更新：

* 从 DEFAULT_BACKEND 密码组中除去了弱密码。
* 支持 Thales nShield® 外部 HSM 前端使用 ECDHE 密码
* 支持 SafeNet 网络外部 HSM 前端使用 ECDHE 密码
* 除去了 SSLv2：从 R12.1 开始，NetScaler VPX 设备不支持 SSLv2。

有关 12.1 SSL 更新的更多详细信息，请参阅 [Citrix 12.1 Release Notes ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}。

### GSLB 的服务组支持
{: #service-groups-support-for-gslb}
现在，您可以为 GSLB 配置基于 IP 地址的服务组、基于域名的服务组或基于域名的自动缩放服务组。您还可以轻松管理一组服务，就像管理单个服务一样，还可将服务组与虚拟服务器绑定，以及向该组添加服务。

有关 GSLB 服务组的更多信息，请参阅 Citrix 文章 [Configuring a GSLB service group ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}。
