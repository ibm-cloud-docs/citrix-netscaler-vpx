---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX 預設部署
{: #citrix-netscaler-vpx-default-deployment}

當您在[客戶入口網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/) 的**裝置 > 裝置清單**中檢視 NetScaler 時，可能會注意到它與其他伺服器不同。亦即，裝置具有「專用 IP 位址」，但沒有「公用 IP 位址」。

{{site.data.keyword.BluSoftlayer_notm}} 上 NetScaler 預設部署的設計旨在盡可能安全，方法是將「專用 IP 位址」自動指派為用於管理的 NetScaler IP (NSIP)。如果您按一下 NetScaler 左側的箭頭，則該行會展開以顯示預設使用者名稱 (root) 及遮罩過的 root 使用者密碼。 

{{site.data.keyword.BluSoftlayer_notm}} 會在佈建期間為您處理大量的決策。例如，哪些 IP 位址用於哪些用途。它會詢問您要將哪些 VLAN 用於部署。此外，它還會使用 Script 及 API 自動進行許多後端配置，例如，將介面指派給個別的公用及專用 VLAN，以及將適當的 IP 位址指派給每一個介面（包括 NSIP、VIP 及 SNIP）。

## 我需要進行哪些配置？

依預設，NSIP 是在佈建期間所指派的「專用 IP 位址」，這是您用來連接至 NetScaler 以進行管理的 IP 位址。依預設，會從相同的「主要 IP 子網路」指派 SNIP（子網路 IP 位址），而此子網路位在您於訂購處理程序期間所選擇的 VLAN 上。 

如果您選擇預期負載平衡伺服器所在的相同 VLAN，則不需要額外配置這些 SNIP。依預設，DNS 會設為 {{site.data.keyword.BluSoftlayer_notm}} 的名稱伺服器。在基本實作中，如果 {{site.data.keyword.BluSoftlayer_notm}} 管理伺服器的 DNS 記錄，則不需要進一步配置。
