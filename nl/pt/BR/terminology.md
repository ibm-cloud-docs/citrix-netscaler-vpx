---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: terminology, nsip, snip, vip, service, object, monitor

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Terminologia do {{site.data.keyword.vpx_full}}
{: #citrix-netscaler-vpx-terminology}

A plataforma Citrix NetScaler usa a terminologia específica do produto e a terminologia básica do balanceador de carga, além de conceitos.

### NetScaler IP (NSIP)
{: #netscaler-ip-nsip-}

O IP do balanceador de carga designado para propósitos de gerenciamento.

### SubNet IP (SNIP)
{: #subnet-ip-snip-}

Um SNIP é o endereço IP de origem de um pacote usado pelo NetScaler sempre que ele deseja se comunicar com um servidor (ou objeto). Os servidores também usam o SubNet IP para responder ao NetScaler.

### IP virtual (VIP)
{: #virtual-ip-vip-}

Um VIP é um endereço IP para o qual um cliente envia solicitações. O NetScaler finaliza a conexão do cliente no VIP e, em seguida, inicia uma conexão com um servidor configurado no serviço de balanceamento de carga.  Isso pode ser um endereço IP público para tráfego público (Internet) ou um endereço IP privado para tráfego privado (intranet).

### Virtual Server
{: #virtual-server}

Um Virtual Server, em termos de balanceamento de carga, refere-se à combinação do endereço IP, da porta e do protocolo ao qual um cliente IP se conecta e onde as solicitações de tráfego são enviadas para um aplicativo específico que está tendo a carga balanceada pelo NetScaler.

### Serviço
{: #service}

A combinação de endereço IP, porta e protocolo usada para rotear solicitações para um servidor específico. Um Serviço, uma vez configurado, deve posteriormente ser associado a um Virtual Server.

### Objeto do servidor
{: #server-object}

Uma entidade virtual que permite designar um nome significativo a um servidor físico, em vez de usar seu endereço IP regular.

### Monitorar
{: #monitor}

Um elemento que permite rastrear um serviço, assegurando que esteja operando corretamente. O monitor usa análises e sinais de pulsação para manter o controle do status de Serviço.
