---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: security, hsm, ntl, certificate

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

# 建立網路信任鏈結 (NTL)
{: #establish-a-network-trust-link-ntl-}

「網路信任鏈結 (NTL)」是 Hardware Security Module (HSM) 和用戶端通訊用的安全通道。NTL 在兩個方向都使用憑證來鑑別及加密 HSM 伺服器分割區與用戶端之間傳輸的資料。

請注意，信任鏈結需要 TCP 埠 1792 同時可供 NTLS 及 NTLA（雙向）通訊協定存取，以保證所有處理程序及公用程式都正常運作。

若要建立 NTL，請執行下列程序：

1.	導覽至 `/var/safenet/safenet/lunaclient/bin` 目錄，並使用 VTL 公用程式來建立憑證。

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	Private Key created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	Certificate created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**附註：**用戶端憑證所用的 ID 是指派給它的專用 IP。這稍後會由 HSM 使用及參照。

2. 使用 SCP 將憑證檔案傳送至 HSM 伺服器：

	```
	root@IBMADC690867-s6dr# scp /var/safenet/safenet/lunaclient/cert/client/	10.121.229.224.pem hsm_admin@10.121.229.201:

	The authenticity of host '10.121.229.201 (10.121.229.201)' can't be established.

	ECDSA key fingerprint is SHA256:UBltOfaDojRlUVxDXh6zI3CPMF8FRaJnls0uxeWgrCY.

	Are you sure you want to continue connecting (yes/no)? yes

	Warning: Permanently added '10.121.229.201' (ECDSA) to the list of known hosts.

	hsm_admin@10.121.229.201's password:

	10.121.229.224.pem                                                 
	100%  818     	
	1.6MB/s   
	00:00
	```

	若要進一步瞭解「虛擬記號程式庫 (VTL)」，請移至 [Utilities Reference Guide ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}。

3.	使用 SCP 將 HSM 伺服器憑證檔案傳送至 {{site.data.keyword.vpx_full}} 用戶端，然後新增伺服器：

	```
	root@IBMADC690867-s6dr# scp hsm_admin@10.121.229.201:server.pem .
	hsm_admin@10.121.229.201's password:

	server.pem                                                         
	100% 1180     	
	2.3MB/s   
	00:00

	root@IBMADC690867-s6dr# vtl addServer -n 10.121.229.201 -c server.pem

	New server 10.121.229.201 successfully added to server list.
	```

	以上所使用的語法如下：

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. 確認新增伺服器：

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	在 HSM 中，執行下列指令以查看任何現有的用戶端：

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs

	Command Result : 0 (Success)
	```

5.	將 VPX 登錄為新的用戶端：

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	'client register' successful.

	Command Result : 0 (Success)
	```

	上一個指令使用下列語法：

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	用戶端名稱不必符合 IBM© Cloud 所指派及使用的 ID，不過建議這麼做以維持名稱一致。

6. 確認已新增用戶端：

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs
	registered client 6: NS-IBMADC690867-s6dr

	Command Result : 0 (Success)
	```

7. 將分割區指派給用戶端。請確定您參照之前建立的分割區。您也必須確定名稱符合前一個步驟中所顯示用戶端的 ID。

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition' successful.

	Command Result : 0 (Success)
	```

	上一個輸出使用下列語法：

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	在 Citrus Netscaler VPX 中驗證連線功能：

	```
	root@IBMADC690867-s6dr# vtl verify

	找到下列 Luna SA 插槽/分割區：

	Slot    Serial #                Label
	====    ================        =====
	0           534071053        partition6
	```

	`vtl verify` 所顯示的輸出應該列出分割區的 "Slot #"、序號，以及連結至此信任鏈結的分割區名稱。任何其他輸出都表示有問題。

	此外，也建議在位於 `/etc` 目錄的 Chrystoki 檔案中，確認憑證及伺服器的路徑。若要這麼做，請執行下列動作：

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

9.	儲存配置：

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	這裡使用的複製指令會讓配置在 VPX 重新開機之後仍然持續存在。

10.	啟動加密作業所需的 safenet 閘道用戶端程序：

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. 確認處理程序正在執行：

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. 最後，確定在重新開機過程中，會自動啟動這個程序：

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

現在，網路信任鏈結已建立。
