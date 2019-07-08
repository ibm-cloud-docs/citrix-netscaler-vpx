---

copyright:
  years: 2019
lastupdated: "2019-04-10"

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

# Criando um túnel de IP
{: #creating-ip-tunnel}

É necessário criar um objeto de túnel de IP para especificar não apenas os endereços IP local e remoto, mas também os parâmetros de protocolo para a conexão VPN. Para isso:

1.	Navegue até **Sistema > CloudBridge Connector > Túneis de IP**.
2.	Na guia **Túneis de IPv4**, clique em **Incluir**.
3.	Digite os seguintes parâmetros:
  *	Name
  *	Remote IP (IP of remote VPN peer)
  *	Remote Mask
4.	Selecione **IP de sub-rede** (SNIP) na lista suspensa IP local.
5.	Escolha o SNIP apropriado a ser usado como o terminal VPN na lista suspensa **IP local**.
6.	Selecione **IPSEC** como o protocolo na lista suspensa.
7.	Escolha o nome do perfil [criado anteriormente](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) na lista suspensa **Nome do perfil IPSec**. 
8.	Clique em **Criar**.

    <img src="images/ipsecCreateIPtunnel.png" alt="desenho" style="width: 200px;"/>

Para criar um túnel de IP na CLI, use a sintaxe a seguir:
  
  ```
  > add ipTunnel IPSec_tunnel1 10.115.168.144 255.255.255.255 10.143.220.106 -protocol IPSEC -ipsecProfileName IPSec_Profile1
  
  ```
