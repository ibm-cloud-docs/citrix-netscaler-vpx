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
{:new_window: target="_blank_"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Establish a Network Trust Link (NTL)
{: #establish-a-network-trust-link-ntl-}

A Network Trust Link (NTL) is a secure channel for the Hardware Security Module (HSM) and the client to communicate. NTLs use certificates in both directions to authenticate and encrypt data transmitted between HSM server partitions and clients.

Be advised that the trust link requires TCP port 1792 to be accessible in both the NTLS and NTLA (bi-directional) protocols to guarantee all processes and utilities work correctly.

To establish your NTL, perform the following procedure:

1.	Navigate to the directory `/var/safenet/safenet/lunaclient/bin` and create the certificate using the VTL utility.

	```
	root@IBMADC690867-s6dr# cd /var/safenet/safenet/lunaclient/bin
	root@IBMADC690867-s6dr# vtl createcert -n 10.121.229.224
	Private Key created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224Key.pem
	Certificate created and written to: /var/safenet/safenet/lunaclient/cert/client/10.121.229.224.pem
	```

	The identifier used for the client certificate is the private IP assigned to it. This will later be used and referenced by the HSM.
  {: note}

2. Transfer the certificate file to the HSM server using SCP:

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

	To learn more about Virtual Token Library (VTL), go to the [Utilities Reference Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Transfer the HSM server certificate file to the {{site.data.keyword.vpx_full}} client using SCP, then add the server:

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

	The syntax used above is the following:

	```
	vtl addServer -n <SA_hostname_or_IP> -c <server_certificate>
	```

3. Confirm the addition of the server:

	```
	root@IBMADC690867-s6dr# vtl listservers
	Server: 10.121.229.201  HTL required: no
	```

4.	In the HSM, execute the following command to see any existing clients:

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

	The previous command uses the following syntax:

	```
	client register -client <client_name> -ip <client_IP_address>
	```

	The client name does not have to match the identifier assigned and used by IBM© Cloud, however, this is recommended to keep names consistent.

6. Confirm the client was added:

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

7. Assign a partition to the client. Make sure you reference the partition created before. You will also have to ensure the name matches the identifier for the client displayed in the previous step.

	```
	[jpmongehsm2] lunash:>client assignPartition -c NS-IBMADC690867-s6dr -p partition6

	'client assignPartition' successful.

	Command Result : 0 (Success)
	```

	The previous output uses the following syntax:

	```
	client assignPartition -client <clientname> -partition <partition name>
	```

8.	Verify connectivity in your Citrus Netscaler VPX:

	```
	root@IBMADC690867-s6dr# vtl verify

	The following Luna SA Slots/Partitions were found:

	Slot    Serial #                Label
	====    ================        =====
	0           534071053        partition6
	```

	The output displayed by `vtl verify` should list the  partition's "Slot #", serial number, and the name of the partition bound to this trust link. Any other output indicates a problem.

	In addition, it's also a good idea to confirm the paths of the certificates and the server in the Chrystoki file located in the `/etc` directory. To do so:

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

9.	Save the configuration:

	```
	root@IBMADC690867-s6dr# cp /etc/Chrystoki.conf /var/safenet/config/
	```

	The copy command used here makes the configuration persistent across reboots in VPX.

10.	Start the safenet gateway client process necessary for cryptographic operations:

	```
	root@IBMADC690867-s6dr# sh /var/safenet/gateway/start_safenet_gw
	```

11. Confirm the process is running:

	```
	root@IBMADC690867-s6dr# ps aux | grep safenet_gw
	root       
	6817  0.0  0.0 10068  1500  ??  Ss    
	4:48PM   
	0:00.00 /var/safenet/gateway/safenet_gw
	```

12. Finally, make sure this process is automatically started during the reboot process:

	```
	root@IBMADC690867-s6dr# touch /var/safenet/safenet_is_enrolled
	```

Your Network Trust Link is now established.
