---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: upgrade, vpx, callhome

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 升级 {{site.data.keyword.vpx_full}}
{: #upgrading-your-citrix-netscaler-vpx}

在尝试此过程之前，您必须先连接到 VPN。
{: note}

1. 登录到 NetScaler 管理 IP。
2. 单击**系统升级**。
4. 从**选择文件**下拉列表中选择**本地**。
4. 从以下位置下载正确的升级文件：

	[NetScaler 可用版本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}

	您必须连接到 IBM© Cloud Infrastructure VPN 才能访问此链接。
  {: note}

5. 在“上传软件”屏幕上，浏览至升级文件的位置，然后单击**升级**。固件将上传。
6. 在所生成的“系统升级”窗口，系统将提示您重新引导。单击**关闭**。
7. 返回至**系统**，并单击**重新引导**。
8. 升级之后，在访问设备之前，关闭所有浏览器实例，并清除计算机的高速缓存。


用户界面根据 NetScaler VPX 的当前版本可能有所不同。
{: note}

如果要从 NetScaler V11 升级到 V12，那么缺省情况下会启用回拨功能，即使您在安装前及安装期间明确禁用此功能也是如此。要禁用此功能，可以使用命令行或 Citrix 管理 UI：

   * 命令行：`disable feature CallHome`
   * Citrix 管理 UI：

     1. 浏览至**配置** > **系统** > **设置**。
     2. 在详细信息窗格中，单击**配置高级功能**链接，然后取消选中**回拨**选项。
     3. 单击**确定**。
     {: note}
