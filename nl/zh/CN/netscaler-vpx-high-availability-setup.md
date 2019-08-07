---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: ha, high availability, setup, configure, configuration

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 设置 {{site.data.keyword.vpx_full}} 以实现高可用性 (HA)
{: #setting-up-citrix-netscaler-vpx-for-high-availability-ha-}

负载均衡器用于对多个应用程序服务器上的流量进行均衡，从而提高可扩展应用程序的性能和稳定性。然而，单个负载均衡器是单点故障。通过配置高可用性 (HA) NetScaler VPX 对可避免此问题。配置 HA 对需要两台 NetScaler VPX 服务器。如果主服务器发生故障，辅助服务器将介入以继续执行负载均衡。

SNIP（子网 IP）被负载均衡的服务器视为向 NetScaler VPX 的 VIP（虚拟 IP）发起的请求（连接）的源 IP。通常，在 HA 对设置中，SNIP 不会更改，但有可能会在故障转移事件期间更改。两个 Netscaler 位于同一子网中时，辅助 NetScaler VPX 的 SNIP 可能会更改为主 NetScaler VPX 初始使用的 SNIP。这不会对处理请求的服务器造成任何混淆。

对于 HA 配置，两个 NetScaler 都必须位于同一 VLAN 和同一子网中。

在开始 HA 配置之前，请确保执行以下先决条件操作：

1. 如果该对将配置为主动-主动，那么添加到实例的任何 VIP 子网的类型都必须为“路由到 VLAN”。
2. 如果该对将配置为主动-被动，那么添加到实例的任何 VIP 子网都必须为“路由到 VLAN”或“辅助路由到 IP" ，并路由到主节点的公共 IP 地址。

在需要的 VLAN 中订购两个 NetScaler VPX 服务器，并订购 VIP 和 SNIP 子网以满足 HA 对配置的先决条件后，可以继续执行以下操作：

1. 打开两个浏览器窗口并登录到两个 NetScaler 上的高级界面。在辅助 NetScaler 上，转至**系统 > 用户管理 > 用户**，并将 root 用户密码设置为与主 NetScaler 相同。然后，在 {{site.data.keyword.BluSoftlayer_notm}} 门户网站的“设备详细信息”页面上，更新文件中的该密码，以匹配为辅助服务器设置的密码。

2. 在要作为辅助的 VPX 上，单击**系统 > 高可用性**，然后右键单击第一行，并单击**编辑**。在“高可用性状态配置”下拉框中，选择**保持辅助**，然后单击**确定**。

3. 选择**添加**。输入其他 VPX 的系统 IP 地址（位于主服务器的“高可用性”选项卡上），然后在底部输入 root 用户登录详细信息。使**启用 INC** 框保留未选中状态。单击**确定**。

	如果收到错误称这些 IP 不在同一子网中，那么可能这两个 VPX 服务器不在同一 VLAN 中。否则，您现在应该能够打开主服务器，并选择**刷新**按钮来查看这两个服务器以高可用性方式运行。

	辅助服务器的新 NetScaler 管理 IP 将比先前的 IP 地址小 1。如果无法获取对辅助 VPX 的任何访问权，请在命令行中使用以下命令除去高可用性：

	`sh ha node`

	然后，除去 ha 节点：

	`rm ha node 1`

4. 在主 VPX 上，您应该会看到现在远程 VPX 正在同步。转至辅助服务器，并检查**网络 > IP** 配置。您应该会看到主服务器的 VIP 和其他 IP 列为被动。

6. 返回到辅助服务器上的**系统 > 高可用性**，然后单击**编辑**。在下拉框中选择**已启用**，然后点击**确定**。

7. 强制执行故障转移以进行测试。刷新屏幕，并观察 IP 地址在辅助服务器上变为活动状态。再次执行故障转移，然后观察它们进入被动状态。对这些 IP 执行 ping 操作以确保有效。

8. 现在，主服务器应该标记为“主”，而辅助服务器应该报告同步状态“成功”。
