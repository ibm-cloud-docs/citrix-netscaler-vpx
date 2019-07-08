---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security

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

# 使用 Citrix Netscaler VPX 部署和配置 IBM Hardware Security Module (HSM)
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

本逐步指南将引导您完成将 HSM 与 Citrix Netscaler VPX 集成的过程。然后，这两个服务就能够通信，并生成创建证书所需的密码资料。

## 关于部署
{: #about-the-deployment}
此部署是使用以下组件规范进行构建和测试的：

|NetScaler VPX 版本和构建|HSM 软件版本|HSM 固件版本|HSM 客户机版本|
| ------------- | ------------- | ------------- | ------------- |
|NS12.1：构建 48.13.nc|6.2.2-5|6.10.9|6.2.2|

如果您拥有更早版本的 VPX，或者如果通过 IBM© Cloud 平台订购设备时仅看到 V11.1 和更低版本作为选择选项，那么可以升级设备，以便可以完成本指南中描述的设置。
{: note}

## 逻辑拓扑
{: #logical-topology}
下图显示了 SSL 卸载用例的网络流量流。这是对 VPX 与 HSM 设备之间信任链路和配置的直观逻辑透视图。

<img src="images/network-flows-logical-topology.jpg" alt="图样" style="width: 700px;"/>

如果您不熟悉 SSL 卸载，请查看此 [Citrix 文章](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html)。

## 需要完成的任务

{: #what-you-ll-accomplish}

在此逐步指南中，您将了解如何使用 Citrix NetScaler VPX 来部署和配置 HSM：

任务|描述
------------- | -------------
[订购 Hardware Security Module (HSM)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-)|首先，您需要订购 HSM。
[订购 Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx)|如果尚未订购 Citrix NetScaler VPX，请进行订购。
[初始化 HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-)|大部分配置需要初始化 HSM 设备。否则，只能执行特定 `show` 命令。
[创建分区](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition)|分区是一种逻辑独立空间，与向 HSM 引擎请求加密对象或在 HSM 引擎中创建加密对象的客户机请求相关联或连接。
[安装 HSM 客户机软件](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software)|在此子部分中，VPX 将随与 HSM 交互所需要的软件和实用程序一起安装。|
[建立网络信任链路 (NTL)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-)|网络信任链路 (NTL) 是 Hardware Security Module (HSM) 与客户机进行通信的安全通道。|
[创建密钥并生成证书签名请求 (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-)|在此子节中，我们将创建一个密钥对，用于生成证书签名请求 (CSR) 并使用该请求来订购/请求证书。|
[订购证书](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate)|为 Citrix NetScaler VPX 订购 SSL 证书。
[检索和传输证书](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate)|检索先前订购的 SSL 证书，以便准备好一切在下一个逐步指南中对 SSL 证书进行安装和配置。
