---

copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: dns, cache, virtual server

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

# 配置 DNS 虚拟服务器
{: #configure-the-dns-virtual-server}

要配置 DNS 虚拟服务器，请执行以下操作：

1. 转至“流量管理”>“负载均衡”>“服务器”。
2. 单击“添加”以添加两个 IBM© Softlayer DNS 解析器 - 10.0.80.11 和 10.0.80.12。

	<img src="images/fp5.png" alt="图样" style="width: 200px;"/> <img src="images/fp5b.png" alt="图样" style="width: 200px;"/>

3. 接下来，通过转至“流量管理”>“负载均衡”>“服务组”并选择“添加”来创建和定义 DNS 服务组。

	<img src="images/fp6.png" alt="图样" style="width: 400px;"/>

4. 选择 DNS 协议，然后单击“确定”。

	<img src="images/fp7.png" alt="图样" style="width: 300px;"/>

5. 在下一个屏幕上，先单击**服务组成员**下的空字段，以将新的 DNS 解析器作为成员服务器添加到此 DNS 服务组。

6. 在“创建服务组成员”面板中，指定 DNS 端口 53，然后单击“创建”。

	<img src="images/fp8.png" alt="图样" style="width: 200px;"/>

7. 单击“关闭”，然后单击“完成”。

	假定可以从 Citrix NetScaler VPX 设备访问这两个 IBM Softlayer DNS 解析器，那么服务组将显示为绿色。

8. 现在，转至“流量管理”>“负载均衡”>“虚拟服务器”，然后单击“添加”以定义 DNS 虚拟服务器。
9. 在“基本设置”下，为虚拟服务器提供名称，选择 DNS 协议和端口 53，然后从专用子网中分配 IP 地址。

	<img src="images/fp9.png" alt="图样" style="width: 300px;"/>

10. 在以下页面上，单击标注了**无负载均衡虚拟服务器服务组绑定**的空字段。
11. 从下拉列表中选择先前定义的 DNS 服务组，然后单击“绑定”。  

	<img src="images/fp10.png" alt="图样" style="width: 300px;"/>

12. 单击“继续”，然后单击“完成”

DNS 虚拟服务器的状态现在应该显示为绿色。

<img src="images/fp11.png" alt="图样" style="width: 500px;"/>
