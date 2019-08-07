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

# {{site.data.keyword.vpx_full}} のアップグレード
{: #upgrading-your-citrix-netscaler-vpx}

この手順を実行する前に、VPN に接続する必要があります。
{: note}

1. NetScaler 管理 IP にログインします。
2. **「システム・アップグレード (System Upgrade)」**をクリックします。
4. **「ファイルの選択」**ドロップダウン・リストから**「ローカル」**を選択します。
4. 以下の場所から正しいアップグレード・ファイルをダウンロードします。

	[NetScaler 使用可能バージョン (NetScaler Available Versions) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}

	このリンクにアクセスするには、IBM© Cloud インフラストラクチャー VPN に接続している必要があります。
  {: note}

5. 「ソフトウェアのアップロード (Upload Software)」画面で、アップグレード・ファイルの場所を表示し、**「アップグレード」**をクリックします。 ファームウェアがアップロードされます。
6. 結果として表示される「システム・アップグレード (System Upgrade)」ウィンドウに、リブートを要求するメッセージが表示されます。 **「閉じる」**をクリックします。
7. **「システム」**に戻り、**「リブート」**をクリックします。
8. アップグレードの後、すべてのブラウザー・インスタンスを閉じ、コンピューターのキャッシュをクリアしてから、アプライアンスにアクセスします。


ユーザー・インターフェースは、NetScaler VPX の現行バージョンによって異なる場合があります。
{: note}

NetScaler バージョン 11 から 12 にアップグレードした場合、インストール前およびインストール中に明確に使用不可にした場合でも、デフォルトで CallHome フィーチャーが使用可能になります。 このフィーチャーを使用不可にするには、コマンド・ラインまたは Citrix 管理 UI を使用します。

   * コマンド・ライン: `disable feature CallHome`
   * Citrix 管理 UI:

     1. **「構成」**>**「システム」**>**「設定」**にナビゲートします。
     2. 詳細ペインで、**「拡張機能の構成 (Configure Advanced features)」**リンクをクリックして、**「Callhome」**オプションのチェック・マークを外します。
     3. **「OK」**をクリックします。
     {: note}
