---
copyright:
  years: 1994, 2018

lastupdated: "2018-06-28"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 升级 Citrix NetScaler VPX

**注：**在尝试此过程之前，您必须先连接到 VPN。

1. 登录到 NetScaler 管理 IP。
2. 单击**系统升级**。
4. 从**选中文件**下拉列表中选择**本地**。 
4. 从以下位置下载正确的升级文件：

	[NetScaler 可用版本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}
	
	**注：**您必须连接到 IBM Cloud Infrastructure VPN 才能访问此链接。

5. 在“上传软件”屏幕上，浏览至升级文件的位置，然后单击**升级**。固件将上载。
6. 在所生成的“系统升级”窗口，系统将提示您重新引导。单击**关闭**。
7. 返回至**系统**，并单击**重新引导**。
8. 升级之后，在访问设备之前，关闭所有浏览器实例，并清除计算机的高速缓存。

**注：**用户界面根据 NetScaler VPX 的当前版本可能有所不同。



