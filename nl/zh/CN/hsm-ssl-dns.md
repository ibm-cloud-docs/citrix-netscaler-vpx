---

copyright:
  years: 2018
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 检查并配置 DNS 记录
{: #check-and-configure-the-dns-record}

在本逐步指南示例中，IBM© Cloud Internet Services 的 DNS 服务用于管理 DNS 区域及其记录。在本例中，必须确保为正在使用的 FQDN 创建记录。该记录应该指向要在 Citrix NetScaler VPX 虚拟服务器中配置的公共地址。

<img src="images/12-add-record.png" alt="图样" style="width: 700px;"/>

在客户门户网站中，通过浏览至**设备 > 设备列表**，然后选择 Citrix NetScaler VPX 的名称，可以检索要用于 Citrix VPX 的静态公共 IP。

<img src="images/13-check-ip.png" alt="图样" style="width: 300px;"/>
