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

# 升級 {{site.data.keyword.vpx_full}}
{: #upgrading-your-citrix-netscaler-vpx}

在嘗試此程序之前，您必須先連接至 VPN。
{: note}

1. 登入「NetScaler 管理 IP」。
2. 按一下**系統升級**。
4. 從**選擇檔案**下拉清單，選擇**本端**。
4. 從下列位置下載正確的升級檔案：

	[NetScaler 可用版本 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}

	您必須連接至 IBM© Cloud Infrastructure VPN 才能存取此鏈接。
  {: note}

5. 在「上傳軟體」畫面上，瀏覽至升級檔案的位置，然後按一下**升級**。韌體將會上傳。
6. 在結果的「系統升級」視窗上，您將會看到重新開機的提示。按一下**關閉**。
7. 回到**系統**，然後按一下**重新開機**。
8. 升級之後，關閉所有瀏覽器實例並清除您電腦的快取，然後才存取應用裝置。


使用者介面可能會視 NetScaler VPX 的現行版本而不同。
{: note}

如果您要從 NetScaler 第 11 版升級至第 12 版，依預設會啟用 CallHome 特性，即使您在安裝之前和期間明確停用它也一樣。如果要停用這項特性，您可以使用指令行或 Citrix 管理使用者介面：

   * 指令行：`disable feature CallHome`
   * Citrix 管理使用者介面：

     1. 導覽至**配置** > **系統** > **設定**。
     2. 在詳細資料窗格中，按一下**配置進階特性**鏈結，然後取消勾選 **CallHome** 選項。
     3. 按一下**確定**。
     {: note}
