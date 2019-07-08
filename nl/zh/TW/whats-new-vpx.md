---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: updates, additions, version

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Citrix NetScaler VPX 的最近更新
{: #recent-updates-for-citrix-netscaler-vpx}

## 12.1 版
{: #version-12-1}

### 具有多個 IP 位址的虛擬伺服器
{: #virtual-servers-with-multiple-ip-addresses}
您現在可以使用多個非連續/連續 VIP IPv4 及 IPv6 位址來建立單一負載平衡虛擬伺服器。連結至虛擬伺服器的每一個 VIP 位址，都被視為個別虛擬伺服器。

如需此特性的相關資訊，請參閱 Citrix 文章 [Multiple IP virtual servers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}。

### SSL
{: #ssl}
已針對 SSL 連線套用下列更新：

* 從 DEFAULT_BACKEND 密碼群組中移除低保護性密碼。
* 支援 Thales nShield® 外部 HSM 前端系統使用 ECDHE 密碼
* 支援 SafeNet 網路外部 HSM 前端系統使用 ECDHE 密碼
* 移除 SSLv2：從 12.1 版開始，NetScaler VPX 應用裝置不支援 SSLv2。

如需 12.1 SSL 更新的詳細資料，請參閱 [Citrix 12.1 版本注意事項 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}。

### GSLB 的服務群組支援
{: #service-groups-support-for-gslb}
您現在可以為 GSLB 配置以 IP 位址為基礎的服務群組、以網域名稱為基礎的服務群組，或以網域名稱為基礎的自動調整服務群組。您也可以像單一服務一樣輕鬆地管理一群服務，並將服務群組連結至虛擬伺服器，以及將服務新增至群組。

如需 GSLB 服務群組的相關資訊，請參閱 Citrix 文章 [Configuring a GSLB service group ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}。
