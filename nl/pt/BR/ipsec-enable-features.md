---

copyright:
  years: 2019
lastupdated: "2019-04-08"

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

# Ativando os recursos necessários no {{site.data.keyword.vpx_full}}
{: #enable-required-features-in-vpx}

É possível ativar os recursos necessários no VPX para criar a VPN IPSec:

1.	Acesse a GUI (interface gráfica com o usuário) do VPX.
2.	Navegue até **Sistema > Configurações > Configurar modos** e ative **Modo da camada 3 (encaminhamento de IP)**.
3.	Acesse **Sistema > Configurações > Configurar recursos avançados** e ative **Cloud Bridge**.

Para ativar esses recursos na CLI, execute os comandos a seguir:

```
> enable ns feature CloudBridge
> enable ns mode L3

```

Para obter instruções adicionais sobre como conectar-se ao NetScaler usando a GUI ou o SSH, visite o [artigo a seguir](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-managing-your-citrix-netscaler-vpx#connecting-to-the-netscaler)
