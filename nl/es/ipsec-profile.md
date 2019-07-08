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

# Crear un perfil de IPSec VPX
{: #creating-ipsec-profile}

El perfil de IPSec incluye parámetros de seguridad para establecer conexiones. Para crear un perfil, realice el procedimiento siguiente:

1.	Vaya a **Sistema > CloudBridge Connector > Perfil de IPSec** y pulse **Añadir**.
2.	Especifique los parámetros siguientes:
  *	**Nombre**
  *	**Algoritmo de cifrado**
  *	**Algoritmo hash**
  *	**Tiempo de vida**
3.	Seleccione la **Versión de protocolo IKE** adecuada.
4.	Si lo desea, marque **Secreto de reenvío perfecto**.
5.	Marque **Existe una clave precompartida** y especifique la PSK en el campo **Valor**.
6.	Pulse **Crear**.

    <img src="images/ipsecCreateProfile.png" alt="dibujo" style="width: 200px;"/>

Para crear un perfil de IPSec en la CLI, utilice la sintaxis siguiente:
  
  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra
  
  ```
