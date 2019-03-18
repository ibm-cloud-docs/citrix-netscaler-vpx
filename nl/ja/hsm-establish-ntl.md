---

copyright:
  years: 2018
lastupdated: "2018-11-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# ネットワーク・トラスト・リンク (NTL) の確立
{: #establish-a-network-trust-link-ntl-}

ネットワーク・トラスト・リンク (NTL) は Hardware Security Module (HSM) および通信するクライアントのセキュア・チャネルです。NTL は両方向で証明書を使用して、HSM サーバーのパーティションとクライアントの間で送信されるデータを認証して暗号化します。

すべてのプロセスとユーティリティーが正しく機能することを保証するために、NTLS および NTLA 両方の (双方向の) プロトコルで TCP ポート 1792 がアクセス可能であることがトラスト・リンクで必要となることに注意してください。

NTL を確立するには、以下の手順を実行します。

1.	ディレクトリー `/var/safenet/safenet/lunaclient/bin` にナビゲートし、VTL ユーティリティーを使用して証明書を作成します。

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	秘密鍵の作成および書き込み先: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	証明書の作成および書き込み先: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**注:** クライアントの証明書に使用される ID は、割り当てられたプライベート IP です。 これは、後で HSM により使用および参照されます。

2. SCP を使用して HSM サーバーに証明書ファイルを転送します。

	```
	root@IBMADC690867-s6dr# scp /var/safenet/safenet/lunaclient/cert/client/	10.121.229.224.pem hsm_admin@10.121.229.201:

	ホスト「10.121.229.201 (10.121.229.201)」の認証性が確立できません。

	ECDSA の鍵指紋は SHA256:UBltOfaDojRlUVxDXh6zI3CPMF8FRaJnls0uxeWgrCY です。

	接続を続行しますか? (はい/いいえ) はい

	警告: 既知のホストのリストに「10.121.229.201」(ECDSA) が永続的に追加されました。

	hsm_admin@10.121.229.201 のパスワード:

	10.121.229.224.pem                                                 
	100%  818     	
	1.6MB/s   
	00:00
	```

	仮想トークン・ライブラリー (VTL) について詳しくは、[「ユーティリティー・リファレンス・ガイド (Utilities Reference Guide)」![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}を参照してください。

3.	SCP を使用して HSM サーバー証明書ファイルを Citrix Netscaler VPX クライアントに転送し、サーバーを追加します。

	```
	root@IBMADC690867-s6dr# scp hsm_admin@10.121.229.201:server.pem .
	hsm_admin@10.121.229.201 のパスワード:

	server.pem                                                         
	100% 1180     	
	2.3MB/s   
	00:00

	root@IBMADC690867-s6dr# vtl addServer -n 10.121.229.201 -c server.pem

	新規サーバー 10.121.229.201 が正常にサーバー・リストに追加されました。
	```

	上記で使用された構文は以下のとおりです。

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. サーバーの追加を確認します。

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	HSM で、次のコマンドを実行して既存のクライアントを確認します。

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs

	コマンド結果 : 0 (成功)
	```

5.	VPX を新規クライアントとして登録します。

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	「client register」が正常に行われました。

	コマンド結果 : 0 (成功)
	```

	上記のコマンドは、以下の構文を使用しています。

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	このクライアント名は、割り当てられ、IBM© Cloud により使用された ID と一致する必要はありません。ただし、名前の整合性を保つことを推奨します。

6. クライアントが追加されたことを確認します。

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs
	registered client 6: NS-IBMADC690867-s6dr

	コマンド結果 : 0 (成功)
	```

7. パーティションをクライアントに割り当てます。 前に作成したパーティションを必ず参照するようにしてください。 また、この名前が前のステップで表示されたクライアントの ID と一致することも確認する必要があります。

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	「client assignPartition」が正常に行われました。

	コマンド結果 : 0 (成功)
	```

	上記の出力は、以下の構文を使用しています。

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	Citrus Netscaler VPX で接続を検証します。

	```
	root@IBMADC690867-s6dr# vtl verify

	以下の Luna SA スロット/パーティションが見つかりました。

	スロット   シリアル #         ラベル
	====    ================        =====
	0           534071053        partition6
	```

	`vtl verify` により表示された出力には、パーティションのスロット番号、シリアル番号、およびこのトラスト・リンクにバインドされたパーティションの名前がリストされるはずです。 他の出力は、問題を示します。

	また、`/etc` ディレクトリーに置かれた Chrystoki ファイル内の証明書とサーバーのパスを確認することもお勧めします。 構成するには、以下の手順に従ってください。

	```
	root@IBMADC690867-s6dr# cd /etc/
	root@IBMADC690867-s6dr# cat /etc/Chrystoki.conf
	Chrystoki2 = {
		LibUNIX64 = /var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so;
		}

	[OUTPUT OMMITED]
		ClientPrivKeyFile = /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem;
		ClientCertFile = /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem;
		ServerCAFile = /var/safenet/safenet/lunaclient/cert/server/CAFile.pem;
		NetClient = 1;
		HtlDir = /var/safenet/safenet/lunaclient/htl/;
		ServerName00 = 10.121.229.201;
		ServerPort00 = 1792;
		ServerHtl00 = 0;
	}
	[OUTPUT OMITTED]
	```

9.	以下のように、構成を保存します。

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	ここで使用されたコピー・コマンドにより、VPX でリブートが行われてもこの構成は持続します。

10.	暗号操作に必要な SafeNet ゲートウェイ・クライアント・プロセスを開始します。

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. プロセスが実行中であることを確認します。

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. 最後に、リブート・プロセス中にこのプロセスが自動的に開始することを確認します。

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

これで NTL が確立されました。
