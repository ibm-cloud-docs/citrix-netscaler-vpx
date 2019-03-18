---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX 缺省部署
{: #citrix-netscaler-vpx-default-deployment}

在[客户门户网站 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/) 上的**设备 > 设备列表**中查看 NetScaler 时，您可能会注意到该设备看起来与其他服务器不同。也就是说，该设备具有专用 IP 地址，但没有公共 IP 地址。

在 {{site.data.keyword.BluSoftlayer_notm}} 上 NetScaler 的缺省部署设计为通过将专用 IP 地址自动分配为用于管理的 NetScaler IP (NSIP)，从而尽可能确保安全。如果单击 NetScaler 左侧的箭头，将展开相应行以显示缺省用户名 (root) 和掩盖的 root 用户密码。 

{{site.data.keyword.BluSoftlayer_notm}} 在供应期间会为您处理大量决策。例如，哪些 IP 地址用于哪些用途。它会询问您希望哪些 VLAN 用于部署。此外，它还会使用脚本和 API 自动执行大量后端配置，例如分配接口以分隔公用和专用 VLAN，并为每个接口分配正确的 IP 地址，包括 NSIP、VIP 和 SNIP。

## 需要配置哪些内容？

缺省情况下，NSIP 是供应期间分配的专用 IP 地址，这是用于连接到 NetScaler 以用于管理的 IP 地址。缺省情况下，会从订购过程中所选 VLAN 上的“主 IP 子网”中分配 SNIP（子网 IP 地址）。 

如果选择了目标负载均衡服务器所在的 VLAN，那么不需要额外配置这些 SNIP。缺省情况下，DNS 设置为 {{site.data.keyword.BluSoftlayer_notm}} 的名称服务器。在基本实现中，如果 {{site.data.keyword.BluSoftlayer_notm}} 托管服务器的 DNS 记录，那么不需要进一步配置。
