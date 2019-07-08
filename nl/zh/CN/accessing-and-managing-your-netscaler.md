---
copyright:
  years: 1994, 2019

lastupdated: "2019-06-11"

keywords: manage, managing, locating, details, portal, device, list

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 管理 Citrix NetScaler VPX
{: #managing-your-citrix-netscaler-vpx}

Citrix NetScaler 设备是功能强大的工具，具有一系列功能，可从多个方面帮助增强和优化 {{site.data.keyword.cloud}} 解决方案。您可以在 {{site.data.keyword.cloud_notm}} 基础架构客户门户网站中找到该设备的信息，还可以连接到该设备并配置其功能。  

## 在客户门户网站中找到 NetScaler 详细信息
{: #locating-netscaler-details-in-the-customer-portal}

Citrix NetScaler 设备列在“设备列表”中，这与您在 {{site.data.keyword.cloud_notm}} 平台上拥有的其他任何服务器一样。

要找到“设备列表”，请执行以下操作：

1. 在浏览器中，打开[客户门户网站 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window} 并登录到您的帐户。
2. 在客户门户网站导航中，选择**设备 > 设备列表**。

您将看到按设备名称排序的各设备。Citrix NetScaler VPX 设备的设备类型为“NetScaler”。

单击 NetScaler 所在行左侧的箭头，以展开该行并显示用于 NetScaler 管理访问的用户名和掩盖的密码。

“设备列表”中列出的其他详细信息包括：

* 位置（NetScaler 所在的数据中心）
* 专用 IP 地址（用于连接到 NetScaler 以执行管理功能）
* 开始日期（机器的订购和供应时间）

门户网站中列出了 NetScaler 的专用 IP 地址，但并未列出 NetScaler 的公共 IP 地址。这是因为对 NetScaler 的管理是使用专用 IP 地址执行的，而 NetScaler 设备的公共 IP 地址用作设备的 VIP 或虚拟 IP，这些地址用于负载均衡服务。
{: note}

## 设备详细信息屏幕
{: #the-device-details-screen}

单击 NetScaler 的名称将转至 NetScaler 的**设备详细信息**页面，其中显示部署了 NetScaler 的 VLAN 以及 NetScaler 的公共 IP 地址。这些 IP 地址是 NetScaler 的缺省公共 VIP 地址，因此不能用于管理。稍后您将使用这些地址来关联到负载均衡服务。

## 连接到 NetScaler
{: #connecting-to-the-netscaler}

{{site.data.keyword.cloud_notm}} 向 NetScaler 设备授予完全 root 用户访问权。要登录到 NetScaler 的管理 UI，您必须连接到 {{site.data.keyword.cloud_notm}} 专用网络（{{site.data.keyword.BluSoftlayer_notm}} 管理 VPN 或从 {{site.data.keyword.cloud_notm}} 环境中服务器上的远程会话执行管理功能）。

要从客户门户网站连接到 NetScaler 的管理 UI，请单击**设备详细信息**屏幕右上角的**操作**下拉列表，然后选择**管理设备**以在浏览器中启动新选项卡或弹出窗口。这会将您路由到 NetScaler 的 NSIP（您先前看到的专用 IP 地址）。显示的页面会要求输入该设备的 root 用户名和密码。一旦输入这些信息，即会转至 NetScaler 管理 GUI。

或者，您可以将 NetScaler 设备的专用 IP 复制并粘贴到 Web 浏览器中。

### NetScaler SSH 访问
{: #netscaler-ssh-access}

您还可以使用最喜爱的 SSH 客户机直接连接到 NetScaler 设备。使用“设备列表”页面中 NetScaler 设备的专用 IP 和登录信息，并确保您已连接到 {{site.data.keyword.cloud_notm}} VPN。
