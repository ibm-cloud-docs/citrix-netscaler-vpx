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

# Estabelecer um Network Trust Link (NTL)
{: #establish-a-network-trust-link-ntl-}

Um Network Trust Link (NTL) é um canal seguro para o Hardware Security Module (HSM) e o cliente se comunicarem. Os NTLs usam certificados em ambas as direções para autenticar e criptografar dados transmitidos entre as partições do servidor HSM e os clientes.

Esteja ciente de que o link de confiança requer que a porta TCP 1792 esteja acessível nos protocolos NTLS e NTLA (bidirecional) para garantir que todos os processos e utilitários funcionem corretamente.

Para estabelecer seu NTL, execute o procedimento a seguir:

1.	Navegue para o diretório `/var/safenet/safenet/lunaclient/bin` e crie o certificado usando o utilitário VTL.

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	Private Key created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	Certificate created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	**NOTA:** o identificador usado para o certificado de cliente é o IP privado designado a ele. Isso será usado e referenciado posteriormente pelo HSM.

2. Transfira o arquivo de certificado para o servidor HSM usando SCP:

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

	Para saber mais sobre a Virtual Token Library (VTL), acesse [Guia de referência de utilitários ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Transfira o arquivo de certificado do servidor HSM para o cliente {{site.data.keyword.vpx_full}} usando SCP e, em seguida, inclua o servidor:

	```
	root@IBMADC690867-s6dr# scp hsm_admin@10.121.229.201:server.pem.
	hsm_admin@10.121.229.201's password:

	server.pem                                                         
	100% 1180     	
	2.3MB/s   
	00:00

	root@IBMADC690867-s6dr# vtl addServer -n 10.121.229.201 -c server.pem

	New server 10.121.229.201 successfully added to server list.
	```

	A sintaxe usada acima é a seguinte:

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. Confirme a inclusão do servidor:

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	No HSM, execute o comando a seguir para ver os clientes existentes:

	```
	[jpmongehsm2] lunash:>client list

	registered client 1: NS-IBMADC690867-d85b
	registered client 2: NS-IBMADC690867-4v36
	registered client 3: NS-jpmongevsi05win2012vsi-4v36
	registered client 4: NS-IBMADC690867-k8ru
	registered client 5: NS-IBMADC690867-wnzs

	Command Result : 0 (Success)
	```

5.	Register the VPX as new client:

	```
	[jpmongehsm2] lunash:>client register -c NS-IBMADC690867-s6dr -ip 10.121.229.224

	'client register' successful.

	Command Result : 0 (Success)
	```

	O comando anterior usa a sintaxe a seguir:

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	O nome do cliente não precisa corresponder ao identificador designado e usado pelo IBM© Cloud, no entanto, isso é recomendado para manter os nomes consistentes.

6. Confirme que o cliente foi incluído:

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

7. Designe uma partição ao cliente. Certifique-se de fazer referência à partição criada antes. Você também terá que assegurar que o nome corresponda ao identificador para o cliente exibido na etapa anterior.

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition' successful.

	Command Result : 0 (Success)
	```

	A saída anterior usa a sintaxe a seguir:

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	Verifique a conectividade em seu Citrus Netscaler VPX:

	```
	root@IBMADC690867-s6dr# vtl verify

	Os slots/partições SA do Luna a seguir foram localizados:

	Slot    Serial #                Label
	====    ================        =====
	0           534071053        partition6
	```

	A saída exibida por `vtl verify` deve listar o "Slot #" da partição, o número de série e o nome da partição vinculada a esse link de confiança. Qualquer outra saída indica um problema.

	Além disso, também é uma boa ideia confirmar os caminhos dos certificados e do servidor no arquivo do Chrystoki localizado no diretório `/etc`. Para isso:

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

9.	Salve a configuração:

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	O comando de cópia usado aqui torna a configuração persistente entre reinicializações no VPX.

10.	Inicie o processo do cliente de gateway do safenet necessário para operações criptográficas:

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. Confirme se o processo está em execução:

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. Por fim, certifique-se de que esse processo seja iniciado automaticamente durante o processo de reinicialização:

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

Agora, seu Link Confiável de Rede está estabelecido.
