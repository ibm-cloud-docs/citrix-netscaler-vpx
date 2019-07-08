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

# Vérification de la connexion d'un tunnel VPN 
{: #verifying-vpn-tunnel-connection}

Exécutez les procédures et commandes suivantes pour vérifier le statut opérationnel de la connexion VPN : 

1.	Confirmez le statut VPN dans VPX en sélectionnant **System > CloudBridge Connector > IP Tunnels**. 

  <img src="images/ipsecVerifyVPN1.png" alt="dessin" style="width: 600px;"/>

  Le statut doit refléter un état **UP** dans l'entrée de tunnel IP respective (**IPSec_tunnel1** dans cet exemple.)

  Pour confirmer le statut de la connexion VPN à l'aide de la CLI, exécutez la commande suivante : 

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

2.	Confirmez le statut VPN dans VRA en exécutant la commande suivante dans la CLI pour confirmer l'état du VPN :
    
  ```
  $ show vpn ipsec sa
  Peer ID / IP                            Local ID / IP
  ------------                            -------------
  10.143.220.106                          10.115.168.144
  
  Tunnel  Id          State  Bytes Out/In   Encrypt       Hash      DH A-Time  L-Time
  ------  ----------  -----  -------------  ------------  --------  -- ------  ------
  1       1           up     0.0/0.0        aes256        sha1      2  18466   86400
  ```

  3.	Testez votre connectivité VPN en émettant un ping depuis l'instance VSI située derrière Citrix VPX vers la VSI du côté distant (dispositif Virtual Router Appliance) :

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
