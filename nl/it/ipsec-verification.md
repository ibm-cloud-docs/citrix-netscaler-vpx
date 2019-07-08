---

copyright:
  years: 2019
lastupdated: "2019-04-28"

keywords: ipsec, vpn, vpx, tunnel

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

# Verifica della connessione tunnel VPN
{: #verifying-vpn-tunnel-connection}

Utilizza i seguenti comandi e procedure per verificare lo stato operativo della connessione VPN:

1.	Conferma lo stato della VPN in VPX andando a **System > CloudBridge Connector > IP Tunnels**.

  <img src="images/ipsecVerifyVPN1.png" alt="immagine" style="width: 600px;"/>

  Lo stato deve riflettere uno stato **UP** nella rispettiva voce del tunnel IP (**IPSec_tunnel1** in questo esempio.

  Per confermare lo stato della connessione VPN utilizzando la CLI, immetti il seguente comando:

  ```    
  > show iptunnel
  1) Domain.......:               0
    Name.........:  IPSec_tunnel1 (TUN1)
    Remote.......:  10.115.168.144   Mask......: 255.255.255.255
    Local........:  10.143.220.106   Encap.....:  10.143.220.106
    Protocol.....:           IPSEC   Type......:               C
    IPSec Profile Name.......:  IPSec_Profile1
    IPSec Tunnel Status......:              UP
    Number of PBRs ..........:               1
      
    Done
      
  ```

2.	Conferma lo stato della VPN nella VRA immettendo il seguente comando nella CLI per confermare lo stato della VPN:
    
  ```
  $ show vpn ipsec sa
  Peer ID / IP                            Local ID / IP
  ------------                            -------------
  10.143.220.106                          10.115.168.144
  
  Tunnel  Id          State  Bytes Out/In   Encrypt       Hash      DH A-Time  L-Time
  ------  ----------  -----  -------------  ------------  --------  -- ------  ------
  1       1           up     0.0/0.0        aes256        sha1      2  18466   86400
  ```

  3.	Verifica la tua connettività VPN immettendo un ping dalla VSI dietro il Citrix VPX alla VSI nel lato remoto (Virtual Router Appliance):

  ```
  >ping 10.115.72.237
  
  Pinging 10.115.72.237 with 32 bytes of data:
  Reply from 10.115.72.237: bytes=32 time=37ms TTL=63
  Reply from 10.115.72.237: bytes=32 time=36ms TTL=63
  Reply from 10.115.72.237: bytes=32 time=35ms TTL=63
  Reply from 10.115.72.237: bytes=32 time=35ms TTL=63
  
  Ping statistics for 10.115.72.237:
      Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
  Approximate round trip times in milli-seconds:
      Minimum = 35ms, Maximum = 37ms, Average = 35ms
  ```
