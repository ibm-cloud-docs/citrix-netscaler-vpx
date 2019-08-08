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

# Configurando a VPN IPSec site-a-site no Citrix NetScaler VPX com o IBM Virtual Router Appliance
{:#configuring-ipsec-site-to-site-vpn-in-citrix-netscaler-vpx}

Este guia fornece instruções passo a passo para configurar uma conexão VPN IPSec site-a-site no Citrix VPX. Um IBM Virtual Router Appliance (VRA) é usado como um peer de VPN.

<img src="images/ipsec1.png" alt="desenho" style="width: 600px;"/>

## Sobre a implementação
Esta implementação foi construída e testada com as seguintes especificações de componente:

| Versão e compilação do NetScaler VPX	| Descrição e versão do VRA | 
| ------------- | ------------- | 
| NS12.1: Build 48.13.nc | AT&T vRouter 5600 1801q |

Uma licença do VPX Platinum é necessária para configurar a VPN IPSec.
{: note}

## Antes
de Começar

Este guia considera a propriedade de ambos os dispositivos. Visite os links a seguir para obter instruções sobre pedidos.

-	[Introdução ao dispositivo de software Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-getting-started)
-	[Introdução ao IBM Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started)

## O que você realizará

Nesse guia, você aprenderá como configurar uma VPN IPSec no dispositivo Citrix VPX.

Tarefa  | Descrição
------------- | -------------
[Ativar os recursos necessários no VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-required-features-in-vpx) | Primeiro, ative os recursos necessários para criar a VPN IPSec.
[Criar o perfil IPSec](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ipsec-profile) | O perfil IPSec inclui parâmetros de segurança para estabelecer a conexão. 
[Criar o túnel de IP](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) | Nesta seção, criamos um objeto de túnel de IP para especificar os endereços IP local e remoto, assim como os parâmetros de protocolo.
[Criar o roteamento baseado em política (PBR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-policy-based-routing) | O PBR é usado para definir os parâmetros exclusivos de tráfego para as sub-redes local e remota.
[Configurar o VRA](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-vra) | Configure o Virtual Router Appliance usando uma sintaxe de configuração de VPN equivalente.
[Verificar o status da VPN](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-verifying-vpn-tunnel-connection) | Verifique o estado da operação da VPN e realize um teste de conectividade simples.

## Recursos Adicionais
Os seguintes recursos adicionais podem ajudá-lo a saber mais sobre o Citrix VPX e o Virtual Router Appliance.

* [CloudBridge Connector ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction.html){:new_window}
* [Configurando u m túnel do CloudBridge Connector entre um dispositivo Citrix ADC e um dispositivo Cisco IOS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/citrix-adc/12-1/system/cloudbridge-connector-introduction/cloudbridge-connector-tunnel-cisco.html){:new_window}
* [Documentação do Citrix VPX/ADC 12.1 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/citrix-adc/12-1){:new_window}
* [Documentação suplementar do VRA](/docs/infrastructure/virtual-router-appliance/vra-docs.html#supplemental-vra-documentation){:new_window}
