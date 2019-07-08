---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, configure, tune, tuning, ssl, offload

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

# 使用 Citrix NetScaler VPX 配置和调整 SSL 卸载
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

本逐步指南将引导您完成在 Citrix NetScaler VPX 中配置和调整 SSL 卸载的过程，这是使用通过 HSM 链接生成的证书和加密资料完成的。

本逐步指南假定您已完成了[使用 Citrix NetScaler VPX 部署和配置 IBM© Hardware Security Module (HSM)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) 中用于订购和创建 VPX/HSM 配对的步骤。
{: note}

## 关于部署
{: #about-the-deployment}
此部署是使用以下组件规范进行构建和测试的：

|NetScaler VPX 版本和构建|HSM 软件版本|HSM 固件版本|HSM 客户机版本|
| ------------- | ------------- | ------------- | ------------- |
|NS12.1：构建 48.13.nc|6.2.2-5|6.10.9|6.2.2|


## 逻辑拓扑
{: #logical-topology}

下图显示了 SSL 卸载用例的网络流量流。这是对 Citrix VPX 与 HSM 设备之间信任链路和配置的直观逻辑透视图。

<img src="images/network-flows-logical-topology.jpg" alt="图样" style="width: 700px;"/>

如果您不熟悉 SSL 卸载，请查看此 [Citrix 文章 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}。

## 需要完成的任务
{: #what-you-ll-accomplish}

在此逐步指南中，您将了解如何使用 Citrix NetScaler VPX 来配置 SSL：

任务|描述
------------- | -------------
[安装证书](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate)|安装您在先前的[逐步指南](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx)中创建的 SSL 证书。
[检查并配置 DNS 记录](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record)|对于指向要在 Citrix NetScaler VPX 中配置为虚拟服务器的公共地址的 FQDN，确保存在 DNS 记录。
[添加和配置 SSL 虚拟服务器](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server)|添加和配置 SSL 虚拟服务器。
[创建并应用新的密码套件](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite)|创建密码套件以对 AEAD、ECDHE 和 ECDSA 划分优先级并设置优先权。

## 其他资源
{: #additional-resources}
以下其他资源可帮助您在使用 IBM Hardware Security Module 时最充分地利用 Citrix NetScaler VPX。

* [NetScaler 12.1 产品文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Gemalto Support Portal ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [IBM Cloud 支持](/docs/get-support?topic=get-support-using-avatar){:new_window}
