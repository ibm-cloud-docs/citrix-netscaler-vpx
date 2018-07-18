---
copyright:
  years: 1994, 2017
  
lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX 软件设备入门

在 {{site.data.keyword.BluSoftlayer_notm}} 解决方案中部署 Citrix NetScaler VPX 可加速 Web 应用程序交付，提升性能，并确保云应用程序和服务保持优化、可用和安全。如果您有挑战性的工作负载（例如，游戏、大数据和分析或私有云），那么 Citrix NetScaler VPX 可以帮助您以用户最需要的时间、地点和方式交付解决方案。

## 开始之前
要开始使用 Citrix NetScaler VPX，您需要了解以下信息：

* 您的 IBM Cloud 客户门户网站登录信息
* 负载均衡器的部署位置
* 哪个 Netscaler 类型最能满足您的需求（有关更多信息，请参阅[负载均衡器一览](https://console.bluemix.net/docs/infrastructure/loadbalancer-service/explore-load-balancers.html)）
* 所需的公共 IP 地址数。
* 要向其分配负载均衡器的 VLAN

## 订购 Citrix NetScaler VPX

要订购 Citrix NetScaler VPX 软件设备，请导航至客户门户网站的订购页面：

1. 在浏览器中，打开[客户门户网站 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window} 并登录到您的帐户。
2. 在客户门户网站导航中，选择**设备 > 设备列表**，然后单击**订购设备**链接。 
3. 在**订购 SoftLayer 产品和服务**页面中，向下滚动到“网络”部分，然后单击 Citrix NetScaler VPX 下的**订购**链接。
4. 从下拉菜单中选择要在其中部署 Citrix NetScaler VPX 软件设备的“位置”。  
5. 选择最适合您的软件修订版、软件版本和吞吐量需求的 NetScaler 类型。 
6. 选择所需的公共 IP 地址数。  
	这些是静态公共 IP 地址，在 NetScaler VPX 上部署为虚拟 IP 地址 (VIP)。
7. 单击**继续**。
8. 为所请求的 IP 地址输入 ARIN（或部署区域中的等效组织）所需的信息。
9. 输入您的联系人信息。 
10. 选择 VLAN。
	要最大限度缩短等待时间并确保优化网络资源利用率，请将 Citrix NetScaler VPX 分配给将分布流量的服务器所在的 VLAN。 
11. 复查订单，接受条款，然后单击**下单**。Citrix NetScaler VPX 软件设备将使用您选择的设置进行部署。 

## 后续工作

您可以了解有关 Citrix Netscaler VPX [功能](about-citrix-netscaler-vpx.html)的更多信息，查看特定 Netscaler [术语](terminology.html)或开始
[配置](netscaler-basic-configuration.html)您的 Netscaler。
