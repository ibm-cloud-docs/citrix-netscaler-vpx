---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, retrieve, transfer, certificate

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

# 检索和转移证书
{: #retrieve-and-transfer-the-certificate}

检索先前订购的 SSL 证书，以便准备好在下一个逐步指南[使用 {{site.data.keyword.vpx_full}} 配置和调整 SSL 卸载](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx)中对其进行安装和配置。

1. 在验证域的所有权后，您应该立即会收到一封电子邮件，确认证书执行和证书本身已完成。

	复制从 `---BEGIN CERTIFICATE---` 开始一直到 `---END CERTIFICATE---` 的文本，并将内容另存为扩展名为 `.cer` 的新证书文件。

2. 将该证书文件复制到 {{site.data.keyword.vpx_full}} 中的 `/nsconfig/ssl` 目录。

  <img src="images/11-transfer-certificate.png" alt="图样" style="width: 600px;"/>

现在，{{site.data.keyword.vpx_full}} 现在已准备就绪，可将证书合并到使用 SSL 的负载均衡部署中。
