---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, ssl, security, add, configure

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

# SSL 仮想サーバーの追加と構成
{: #add-and-configure-the-ssl-virtual-server}

SSL 仮想サーバーを追加および構成するには、以下の手順を行います。

1. **「システム」>「設定」>「基本フィーチャーの構成 (Configure Basic Features)」**にナビゲートします。 **「SSL オフロード」**を選択し、**「OK」**をクリックします。
2. NetScaler GUI で、**「トラフィック管理 (Traffic Management)」>「ロード・バランシング (Load Balancing)」>「サービス (Services)」>「追加 (Add)」**にナビゲートし、名前、IP アドレスを指定して、プロトコルを**「HTTP」**に設定します。 **「OK」**を押して終了します。
3. サービスが操作可能であることを確認します。

	<img src="images/15-confirm-service.png" alt="図面" style="width: 700px;"/>

4. 追加サーバー用にステップ 2 を繰り返します。
5. **「トラフィック管理 (Traffic Management)」>「ロード・バランシング (Load Balancing)」>「仮想サーバー (Virtual Servers)」>**にナビゲートし、**「追加 (Add)」**をクリックします。 名前を指定し、プロトコルとして**「SSL」**を選択し、パブリック IP アドレスを入力します。**「OK」**を押して終了します。
6. **「ロード・バランシング仮想サーバーのサービス・バインディングなし (No Load Balancing Virtual Server Service Binding)」**を選択し、**「選択」**をクリックします。 以前のステップで作成したサービスを選択し、「選択」をクリックしてから、**「バインド/続行 (Bind/Continue)」**をクリックします。

	<img src="images/18-bind-service.png" alt="図面" style="width: 700px;"/>

7. 最後に、**「サーバー証明書なし (No Server Certificate)」**をクリックし、次に**「サーバー証明書の選択 (Select Server Certificate)」**をクリックし、以前にインストールした証明書を選択します。 **「選択」**をクリックし、次に**「バインド/続行 (Bind/Continue)」**をクリックし、最後に**「完了」**をクリックして終了します。
