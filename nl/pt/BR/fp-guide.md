---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: proxy, traffic, appliance

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

# Configurando o redirecionamento de tráfego de proxy de encaminhamento usando o dispositivo Citrix NetScaler VPX
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

Este guia fornece uma configuração passo a passo para uma configuração de proxy de encaminhamento usando o dispositivo Citrix NetScaler VPX. Essa configuração foi testada em um dispositivo Citrix NetScaler VPX que estava executando uma versão de software 11.1 (edição de recurso Platinum) e com um desempenho de 10 Mbps.

<img src="images/fp1.png" alt="drawing" style="width: 600px;"/>

## O que você realizará
{: #what-you-ll-accomplish}

Neste guia passo a passo, você aprenderá a configurar o serviço:

Tarefa  | Descrição
------------- | -------------
[Fazer o pedido do Citrix NetScaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) | Comece fazendo o pedido de um dispositivo Citrix NetScaler VPX.
[Solicitar uma sub-rede privada](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) | Solicite ao Suporte IBM© uma sub-rede privada para sua conta.
[Ativar recursos de Redirecionamento de cache e de Balanceamento de carga](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) | Identifique os recursos de seu aplicativo, tais como conjuntos de origem e mecanismos de verificação de funcionamento.
[Configurar o DNS Virtual Server](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) | Inclua seus resolvedores DNS, defina seu grupo de serviços DNS e, em seguida, defina seu DNS Virtual Server.
[Configurar o tráfego de Redirecionamento de cache para HTTP(S)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-traffic) | Configure o redirecionamento de cache para o servidor virtual proxy de encaminhamento com tráfego HTTP ou HTTPS.
[Configurar o tráfego de Redirecionamento de cache para SSL (opcional)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) | Configure o redirecionamento de cache para o servidor virtual proxy de encaminhamento com tráfego SSL em vez de HTTP ou HTTPS.
[Configurar a NAT de origem para o tráfego de saída](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) | Utilize o dispositivo Citrix NetScaler VPX para executar a NAT no tráfego de saída das máquinas do cliente.
[Atualizar as Configurações de proxy no navegador da Internet da máquina do cliente (opcional)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) | Atualize as configurações de proxy usando o navegador da Internet da máquina do cliente, se desejar.
