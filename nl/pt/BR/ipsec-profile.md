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

# Criando o VPX do perfil IPSec
{: #creating-ipsec-profile}

O perfil IPSec inclui parâmetros de segurança para estabelecer conexões. Para criar um perfil, execute o seguinte procedimento:

1.	Navegue até **Sistema > CloudBridge Connector > Perfil IPSec** e clique em **Incluir**.
2.	Digite os seguintes parâmetros:
  *	**Name**
  *	**Encryption Algorithm**
  *	**Hash Algorithm**
  *	**Lifetime**
3.	Selecione a **Versão do protocolo IKE** apropriada.
4.	Marque **Perfect Forward Secrecy**, se desejar.
5.	Marque **Chave pré-compartilhada existente** e insira o PSK no campo **Valor**.
6.	Clique em **Criar**.

    <img src="images/ipsecCreateProfile.png" alt="desenho" style="width: 200px;"/>

Para criar um perfil IPSec na CLI, use a sintaxe a seguir:
  
  ```
  > add ipsec profile IPSec_Profile1 -ikeVersion V1 -encAlgo AES256 -hashAlgo HMAC_SHA1 -lifetime 86400 -psk ipsecpskvpxvra
  
  ```
