---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"

keywords: order, vpx, overview

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Introdução ao dispositivo de software {{site.data.keyword.vpx_full}}
{: #getting-started}

A implementação de um {{site.data.keyword.vpx_full}} em sua solução do {{site.data.keyword.BluSoftlayer_notm}} acelera a entrega de aplicativos da web, impulsiona o desempenho e assegura que seus aplicativos e serviços em nuvem permaneçam otimizados, disponíveis e seguros. Se você tiver cargas de trabalho desafiadoras, como jogos, big data e analítica ou nuvens privadas, o {{site.data.keyword.vpx_full}} poderá ajudá-lo a entregar sua solução quando, onde e como seus usuários precisarem mais.

## Antes
de Começar
{: #before-you-begin}
Para começar a usar o {{site.data.keyword.vpx_full}}, será necessário saber as informações a seguir:

* Suas informações de login do Portal do cliente do IBM© Cloud
* O local de implementação para o balanceador de carga
* Qual tipo de NetScaler é o mais adequado às suas necessidades (para obter mais informações, consulte [Explorar Load Balancers](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)
* O número de endereços IP públicos necessários
* A VLAN na qual você deseja designar o balanceador de carga

## Solicitando um {{site.data.keyword.vpx_full}}
{: #ordering-a-citrix-netscaler-vpx}

Para solicitar um dispositivo de software {{site.data.keyword.vpx_full}}, navegue para a página de pedido no Portal do cliente:

1. Em seu navegador, abra [Portal do Cliente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window} e efetue login em sua conta.
2. Na navegação do Portal do cliente, selecione **Dispositivos > Lista de dispositivos** e clique no link **Pedir dispositivos**.
3. Na página **Pedir produtos e serviços SoftLayer**, role para baixo até a seção Rede e clique no link **Pedir** sob {{site.data.keyword.vpx_full}}.
4. Selecione um Local no menu suspenso no qual você gostaria de implementar o dispositivo de software {{site.data.keyword.vpx_full}}.  
5. Selecione o melhor tipo de NetScaler para sua edição de software, versão de software e necessidades de rendimento.
6. Selecione o número de endereços IP públicos necessários.  
	Estes são endereços IP público estáticos, implementados como endereços IP virtuais (VIPs) no NetScaler VPX.
7. Clique em **Continue**.
8. Insira as informações requeridas por ARIN (ou a organização equivalente em sua região de implementação) para os endereços IP solicitados.
9. Insira suas informações de contato.
10. Selecione sua VLAN.
	Para minimizar a latência e assegurar a utilização otimizada de seus recursos de rede, designe o {{site.data.keyword.vpx_full}} à mesma VLAN dos servidores nos quais o tráfego será distribuído.
11. Revise o pedido, aceite os termos e clique em **Fazer pedido**. O dispositivo de software {{site.data.keyword.vpx_full}} é implementado com suas configurações selecionadas.

## O que vem a seguir
{: #what-s-next}

É possível saber mais sobre os [recursos](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-about-citrix-netscaler-vpx) do {{site.data.keyword.vpx_full}}, revisar a [terminologia](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-citrix-netscaler-vpx-terminology) específica do Netscaler ou começar a [configurar](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-basic-load-balancing-configuration) o seu Netscaler.
