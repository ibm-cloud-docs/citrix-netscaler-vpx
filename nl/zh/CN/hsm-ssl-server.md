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

# 添加和配置 SSL 虚拟服务器
{: #add-and-configure-the-ssl-virtual-server}

要添加和配置 SSL 虚拟服务器，请执行以下过程：

1. 浏览至**系统 > 设置 > 配置基本功能**。选择 **SSL 卸载**，然后单击**确定**。
2. 在 NetScaler GUI 中，浏览至**流量管理 > 负载均衡 > 服务 > 添加**，然后指定名称和 IP 地址，并将协议设置为 **HTTP**。点击**确定**以完成。
3. 确认该服务是否正常运行：

	<img src="images/15-confirm-service.png" alt="图样" style="width: 700px;"/>

4. 对其他任何服务器重复步骤 2。
5. 浏览至**流量管理 > 负载均衡 > 虚拟服务器 >**，然后单击**添加**。指定名称，并指定 **SSL** 作为协议，然后输入公共 IP 地址。点击**确定**以完成。
6. 现在，选择**无负载均衡虚拟服务器服务绑定**，然后单击**选择**。选择在先前步骤中创建的服务，单击“选择”，然后单击**绑定/继续**。

	<img src="images/18-bind-service.png" alt="图样" style="width: 700px;"/>

7. 最后，单击**无服务器证书**，单击**选择服务器证书**，然后选择您先前安装的证书。单击**选择**，单击**绑定/继续**，然后单击**完成**以完成。
