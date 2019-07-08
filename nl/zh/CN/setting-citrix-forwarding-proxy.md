---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"

keywords: setup, proxy, forward, vip, subnet

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 将 Citrix Netscaler VPX 设置为转发代理
{: #setting-up-citrix-netscaler-vpx-as-a-forwarding-proxy}

转发代理充当内部网络和因特网上的客户机之间的单控制点。通过该代理，网络或安全性管理员有能力创建策略来限制对因特网站点的访问。

内部网络上的客户机发起请求时，代理的 IP 地址将用于发起对因特网上远程服务器的请求。远程服务器会转而响应代理，然后代理再将响应返回给客户机。

通常，代理与防火墙组合使用，以确保内部网络中客户机的安全性。

## 步骤 1：请求要在专用网络中使用的 VIP
{: #step-1-request-vips-to-use-in-the-private-network}

在 {{site.data.keyword.BluSoftlayer_notm}} 客户门户网站中订购 Citrix NetScaler VPX 负载均衡器时，假定请求的是逆向代理。将要求请求者提供要用作虚拟 IP (VIP) 的“公共”IP 数。

对于转发代理，需要在专用网络上设置 VIP。需要开具支持凭单，以便请求专用网络的多个 VIP。所需的 VIP 数将决定凭单中所请求子网的大小。凭单中将返回子网信息。

在示例中，我们请求了 `/29` 子网，因此获得以下结果：

* 创建了子网 `10.114.27.0/29` 以用作专用 VIP

* 子网 IP (SNIP) `10.114.52.101` 和路由子网 `10.114.27.0/29`

* 支持团队向 Citrix NetScaler VPX 添加了 VIP `10.114.27.0-3`

## 步骤 2：在 Citrix NetScaler VPX 上启用负载均衡和高速缓存重定向功能
{: #step-2-enable-load-balancing-and-cache-redirect-features-on-the-citrix-netscaler-vpx}

缺省情况下，Citrix NetScaler VPX 负载均衡器上的负载均衡和高速缓存重定向功能已禁用；`enable ns feature cr lb` 命令可启用这两个功能。


## 步骤 3：创建转发代理
{: #step-3-create-the-forward-proxy}

使用命令行对 Citrix NetScaler VPX 发出以下命令。在我们的场景中，仅添加两个 {{site.data.keyword.BluSoftlayer_notm}} DNS 服务器中的一个服务器。  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

第 1 行用于创建重定向高速缓存。协议为 HTTP，`10.114.27.3` 是专用网络上请求的其中一个 VIP。端口是 HTTP 的缺省端口 80 ，但由于此地址和端口组合将用作浏览器中的代理语句，因此可以将此端口更改为任何所需的端口。

第 2 行用于添加将代表“实际”DNS 的负载均衡 VIP。

第 3 行用于将“实际”DNS 的 IP 地址添加为服务。此地址可以是客户 DNS，或者可以路由回 {{site.data.keyword.BluSoftlayer_notm}} 提供的 DNS 解析器。

第 4 行用于将 VIP 绑定到“实际”服务器。所有对 `10.114.27.4` 的 DNS 请求都将发送到 `10.0.80.12`。

第 5 行用于指示转发代理虚拟服务器使用虚拟 DNS 进行名称解析。

## 配置客户机
{: #configuring-the-client}

在继续定制客户机以使用转发代理之前，请确保无法在客户机上使用 Firefox 浏览器来访问公共站点（例如 http://www.ibm.com）。因为客户机上不应该有公共接口，所以此请求应该会失败。

以下示例将配置 Linux 客户机。

需要对客户机进行一些更改。第一个更改是将客户机上的解析器指向虚拟 DNS，这可以通过两种方式之一来执行。

可以手动编辑 `/etc/resolv.conf` 以指向 DNS 的虚拟地址。请注意，客户机管理工具可能会将这些更改恢复为原始设置。  

或者，可以编辑 `/etc/sysconfig/network-scripts/ifcfg-ethx` 接口并添加 `DNS1=` 语句。一旦设置后，就可以发出服务网络重新启动命令来获取更改。

在任一情况下，都需要将 DNS IP 地址配置为虚拟 DNS 地址，并且需要将客户机的浏览器配置为将请求指向 Citrix NetScaler VPX 转发代理。

在 Firefox 中使用以下步骤进行必要的更改：

1. 单击**首选项 > 高级 > 网络 > 连接设置**。

* 选择**手动代理配置**，然后输入以下内容：

  * **地址：**10.114.27.3

  * **端口：**80

  * 选中**对所有协议使用此代理服务器**复选框。

* 单击**保存**并关闭浏览器窗口。

IP 地址 `10.114.27.3` 是在步骤 1 中创建的转发高速缓存的 IP 地址。

到此设置已完成，您可以通过专用网络上隔离的资源来访问因特网。

## 验证设置
{: #validating-the-setup}

现在，客户机已配置为使用转发代理，请重试访问公共站点。请求现在应该会成功。

以下显示命令可用于验证转发代理的状态。

**show cr policy：**显示所有现有的高速缓存重定向策略。

**show policy map：**显示已配置的映射策略以及相关的映射策略信息。

**show cr vserver：**显示指定的高速缓存重定向虚拟服务器或所有已配置的高速缓存重定向虚拟服务器。

**stat cr vserver：**显示高速缓存重定向 Vserver 统计信息。

Citrix 上的基本转发代理的配置相当简单。它为内部网络上的客户机访问因特网上的资源提供了一条安全路径。此外还支持网络管理员维护对网络的控制级别。

如果是在客户站点上实现，建议向配置添加防火墙，以进一步保护资源。
