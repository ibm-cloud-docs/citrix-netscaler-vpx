---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: gslb, vpx, cdn, object storage

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 全局负载均衡
{: #global-load-balancing}

全局服务器负载均衡 (GSLB) 方法使用 DNS 和地理位置来确定应该将服务器流量发送到哪里，从而将流量分布到多个服务器。通常，全局负载均衡器将客户机请求发送到更靠近客户机的服务器，从而减少等待时间并提高性能。

您可能并不需要全面实现全局负载均衡解决方案。GSLB 需要的是可执行此功能的适用设备的多个实例，根据您的需求，其他解决方案可能更具吸引力。如果需要整个 Web 站点和应用程序，那么 GSLB 是不错的选择。如果您只需要内容的一部分（例如，图像、视频或其他大型文件），那么[内容交付网络](/docs/infrastructure/CDN?topic=CDN-about-content-delivery-networks-cdn-)可能更适用（并且更易于部署）。

## Citrix NetScaler VPX
{: #citrix-netscaler-vpx}

Citrix NetScaler VPX 是唯一执行真正全局负载均衡的客户可配置设备。NetScaler 是一种多功能设备，可以执行基于 DNS 的全局负载均衡查找。您可以指向作为 DNS 服务器的 NetScaler，该设备将检查自己配置为对其执行负载均衡的服务器，执行距离计算，并返回一个记录，其中包含与客户机请求最靠近的服务器的 IP。

对于全局负载均衡，您将在每个数据中心进行 NetScaler 设备配置。每个 NetScaler 设备配置可能具有单个 Netscaler 或一对 Netscaler（HA 对），具体取决于您的需求，为其后面的服务器提供本地负载均衡服务。这些设备配置为相互交流，因此它们可交换分配给全局负载均衡器循环的每个服务器的状态信息。到达这些已配置 NetScaler 的任何 DNS 请求都可以返回联机并有响应的服务器的相应记录。任何无响应的服务器都会从循环中除去，然后选择另一个服务器。

您必须已设置负载均衡，即便均衡的服务器只有一台。对于某些服务，您需要额外的 IP 地址，即 GSLB 站点 IP。此 IP 由 NetScaler 用于与全局负载均衡协议中的其他 NetScaler 进行通信。

以下全局均衡过程使用：

### VPX1
{: #vpx1}

`50.97.235.236` 名为 `VPX1Vserver`，是该设备的本地负载均衡 VIP。`50.23.66.52` 将称为 `VPX1site`，是该设备 GSLB 的本地 IP。

### VPX2
{: #vpx2}
`208.43.241.249` 用于 `VPX2Vserver`，GSLB IP 为 `208.43.224.4`，称为 `VPX2site`。

1. 转至**流量管理 > GSLB**，然后右键单击以启用该功能。接下来，选择**站点**和**添加**。

2. 在第一个设备上，在“名称”中输入 VPX1，“类型”为本地，IP 为 `50.23.66.52`，然后选择**关闭**。

	您应该会看到该站点列出并且状态为绿色。暂不要添加远程站点。

3. 转至**流量管理 > GSLB**，然后选择 **GSLB 向导**。单击**下一步**。输入将对其进行负载均衡的主机名（在此示例中，输入 `gslb.tsstesting.com`）。使“记录类型”保留为 A，“服务类型”保留为“任意”。虚拟服务器名称将自行填充。单击**下一步**。

4. 就像使用常规负载均衡一样，选择均衡形式和持久性方法。单击**下一步**。

5. 站点已填充，因此您不必添加任何内容。请改为单击第一个站点的名称旁边的绿色“+”。从列表中选择该设备上的 Vserver，然后单击**创建**。您应该会看到该站点已配置了站点 IP 以及负载均衡设置的 Vserver IP，并且该站点为绿色。单击**下一步** > **完成** > **退出**。

6. 使用该服务器的值对下一个 NetScaler 执行相同的操作。

7. 在两台服务器上，转至**流量管理 > DNS > 记录 > A 记录**，然后检查列表。您应该会看到类型为 `GSLB 域`的 `root.servers.net` 条目，以及主机名。

8. 转至**流量管理 > DNS > 名称服务器**，然后单击**添加**。在 NetScaler 上输入 IP 地址（例如，设备的公共 IP）。单击**本地**，并使协议保留为 UDP。单击**创建**，然后单击**关闭**。您应该会看到有效状态为已启用并运行。

9. 转至**系统 > 网络 > IP**，然后打开 GSLB IP 地址。确保为这两台机器选择**管理**。

10. 接着，在两台服务器上，返回到**流量管理 > GSLB**，然后再次执行向导。这一次，请单击**下一步**，然后选择**修改现有域的配置**。从列表中选择主机名，然后单击两次**下一步**。

11. 在“站点地址”字段中，放入另一个 NetScaler 的站点 IP 地址，并为其提供另一个 NetScaler 的站点名称，然后单击**添加**。这将使用可单击绿色“+”的选项再次填充该站点。单击远程站点加号以添加另一个站点。输入 Vserver 服务 IP（负载均衡服务器的相应 IP，而不是 GSLB 站点 IP）和端口，单击**创建** > **关闭** > **下一步** > **完成**，然后单击**退出**。

如果到目前为止一切顺利，并且已配置了两个服务器，那么在“GSLB 虚拟服务器”、“服务”和“站点”中，所有项的状态都应该是绿色。如果两个机器已正确同步，那么您会注意到，这两个机器上的 GSLB 服务中现在有两个条目。此时，服务器正在相互通信。

现在必须配置 DNS。

在 `gslb.tsstesting.com` 示例中，您将在 tsstesting.com 区域中创建 NS 和粘接记录：

    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; nameserver IP of first NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; nameserver IP of second NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias to the GSLB object on the NetScaler appliance

请记住，您只能将 CNAME 用于主机名，而不能将其用于域的根目录。

此配置会设置名称服务器，以将对 `gslb.tsstesting.com` 的请求转至在其上已配置 DNS 的 NetScaler IP。CNAME 记录将 `tsstesting.com` 转换为对 `gslb.tsstesting.com` 的请求。随后，对 `www.tsstesting.com` 的任何请求都将转至 NetScaler 进行解析，并将基于所配置的负载均衡方法返回记录。

有关 NetScaler 全局负载均衡的更多信息，请参阅：
* [配置 Netscaler 以进行全局负载均衡 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://support.citrix.com/article/CTX110348){: new_window}
* [How DNS(Domain Name System) works with GSLB feature on NetScaler ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://support.citrix.com/article/CTX122619){: new_window}
* [Information on the MEP protocol and site monitoring ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://support.citrix.com/article/CTX111081){: new_window}

有其他产品可以提供类似的功能，以基于地理位置来分布流量：

### CDN
{: #cdn}

内容交付网络（CDN）支持向地理上分散的高速缓存服务器上传或提供源服务器，然后由高速缓存服务器将内容提供给请求客户机。CDN 最适用于静态批量内容，例如不会随时间更改的图像和视频。

有关 CDN 的更多详细信息，请参阅[此文档](/docs/infrastructure/CDN?topic=CDN-getting-started)。

### Object Storage
{: #object-storage}

{{site.data.keyword.BluSoftlayer_notm}} 的 Object Storage 可配置为在各种数据中心使用多个地理位置来提供内容。可感知地理位置的应用程序可以对客户机请求执行位置查找，然后返回靠近客户机的 Object Storage 的 URL。Object Storage 还可根据需要随附 CDN 前端，以提供如上所述的额外高速缓存服务。

有关 Object Storage 的更多信息和简介，请参阅[此文档](/docs/services/cloud-object-storage?topic=cloud-object-storage-about)。
