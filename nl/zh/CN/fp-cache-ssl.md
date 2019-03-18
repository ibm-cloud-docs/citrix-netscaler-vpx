---



copyright:
  years: 2017
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 为 SSL 流量配置高速缓存重定向（可选）
{: #configure-cache-redirection-for-ssl-traffic-optional-}

您可能希望将使用 HTTP 或 HTTPS 协议的虚拟服务器定义为处理 SSL 流量，而不为其定义高速缓存重定向（如先前步骤中所述）。 

为此，请执行以下步骤：

1. 转至**流量管理 > 高速缓存重定向 > 虚拟服务器**，然后单击**添加**。指定正向代理虚拟服务器的名称，选择 SSL 协议和**正向**高速缓存类型。为其分配专用子网中的 IP 地址及其必需端口。 

	<img src="images/fp14.png" alt="图样" style="width: 300px;"/>

	单击**确定**。 
	
2. 查看摘要页面，然后单击**确定**以继续。
3. 指定“重定向”、“DNS 虚拟服务器”和“目标虚拟服务器”配置。 
4. 单击**高级设置**面板下的**证书**以查看与 SSL 证书相关的配置。 
5. 单击空字段**无服务器证书**。
6. 从“选择服务器证书”下拉列表中，选择您的 SSL 服务器。
7. 根据需要输入证书配置信息。

	<img src="images/fp15.png" alt="图样" style="width: 400px;"/>

	单击**安装**。
	
8. 选择**绑定**。

	<img src="images/fp16.png" alt="图样" style="width: 300px;"/>
