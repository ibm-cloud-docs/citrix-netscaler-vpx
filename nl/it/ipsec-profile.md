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

# Creazione di un VPX profilo IPSec 
{: #creating-ipsec-profile}

 Il profilo IPSec include dei parametri di sicurezza per stabilire le connessioni. Per creare un profilo, esegui la seguente procedura:

1.	Passa a **System > CloudBridge Connector > IPSec Profile** e fai clic su **Add**.
2.	Immetti i seguenti parametri:
  *	**Name**
  *	**Encryption Algorithm**
  *	**Hash Algorithm**
  *	**Lifetime**
3.	Seleziona il valore appropriato per **IKE Protocol Version**.
4.	Seleziona **Perfect Forward Secrecy** se lo desideri.
5.	Seleziona **Pre-Shared Key Exists** e immetti la PSK nel campo **Value**.
6.	Fai clic su **Create**.

    <img src="images/ipsecCreateProfile.png" alt="immagine" style="width: 200px;"/>

Per creare un profilo IPSec nella CLI, utilizza la seguente sintassi:
  
  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra
  
  ```
