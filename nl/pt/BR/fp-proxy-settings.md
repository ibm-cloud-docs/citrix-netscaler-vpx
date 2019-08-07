---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: proxy, update

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

# Atualizar as Configurações de proxy no navegador da Internet da máquina do cliente (opcional)
{: #update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-}

Para atualizar as configurações de proxy usando o navegador da Internet da máquina do cliente, execute as etapas a seguir:

1. Acesse **Opções da Internet** em suas configurações do navegador e configure-o para usar um servidor proxy para solicitações realizadas.
2. Use o endereço IP de seu servidor virtual de redirecionamento de cache que foi definido em etapas anteriores como o seu proxy.

Essas configurações de proxy podem não ser necessárias se o dispositivo {{site.data.keyword.vpx_full}} estiver no caminho direto da camada 3 entre as máquinas do cliente e a Internet.
{: note}

<img src="images/fp17.png" alt="drawing" style="width: 500px;"/>
