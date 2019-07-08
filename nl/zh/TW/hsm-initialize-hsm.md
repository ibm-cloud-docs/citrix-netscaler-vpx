---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, initialize

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

# 起始設定 IBM Hardware Security Module (HSM)
{: #initialize-ibm-hardware-security-module-hsm-}

大部分配置需要起始設定 HSM 裝置。若沒有，則只能執行某些 `show` 指令。

若要起始設定您的裝置，請遵循下列步驟：

1.	利用控制入口網站的**裝置 > 裝置清單 > 展開 HSM 名稱**下列出的認證，使用 SSH 連接到 IBM© Hardware Security Module 裝置。

	或者，您可以使用公開金鑰鑑別。如需相關資訊，請檢閱 [Appliance Administration Guide（第 38 頁）![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}。

	依預設，通常會啟用並容許 SSH 存取。如果您在使用 SSH 進行連接時發生問題，請檢查基礎架構的遞送和安全。
  {: note}

2. 執行 `hsm init` 指令：

	```
	[jpmongehsm2] lunash:>hsm init -l jpmonge

	Please enter a password for the HSM Administrator:
	> ********

	Please re-enter password to confirm:
	> ********

	Please enter a cloning domain to use for initializing this HSM:
	> ********

	Please re-enter cloning domain to confirm:
	> ********

	CAUTION:  Are you sure you wish to initialize this HSM?

	Type 'proceed' to initialize the HSM, or 'quit'
		to quit now.
		> proceed
		'hsm init' successful.

	Command Result : 0 (Success)
  	```

	其中，使用的語法為：`hsm init -l <hsmlabel>`

`-l` 參數或標籤是用來指派 ID 給 HSM 的參數，並且可以是與業務、管理者或其履行角色相關的任何有意義的文字或說明。HSM 管理者密碼會是「HSM 安全管理者 (SO)」的指定密碼，基本上是建立和配置加密物件以及變更 HSM 環境所需的設定檔。

最後，複製網域是共用的 ID，可讓物件在一組 HSM 之間形成。這通常用於備份及/或 HA。

如需 HSM CLI 中支援的所有可用指令，請參閱 [LunaSH Command Reference Guide![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window}。
