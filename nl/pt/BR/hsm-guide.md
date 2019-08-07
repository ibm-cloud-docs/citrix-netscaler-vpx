---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security

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

# Implementando e configurando o IBM Hardware Security Module (HSM) com o {{site.data.keyword.vpx_full}}
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

Este Passo a passo o guia ao longo do processo de integração do HSM com o {{site.data.keyword.vpx_full}}. Os dois serviços serão, então, capazes de se comunicar e gerar o material criptográfico necessário para criar um certificado.

## Sobre a implementação
{: #about-the-deployment}
Esta implementação foi construída e testada com as seguintes especificações de componente:

| Versão e compilação do NetScaler VPX	| Versão do Software HSM | Versão do firmware do HSM | Versão do cliente do HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

Se tiver uma versão mais antiga do VPX ou se visualizar apenas as versões 11.1 e anteriores como opções de seleção ao solicitar o dispositivo por meio da plataforma IBM© Cloud, o dispositivo poderá passar pelo upgrade para que a configuração descrita neste guia possa ser concluída.
{: note}

## Topologia Lógica
{: #logical-topology}
O diagrama abaixo mostra o fluxo de tráfego de rede para o caso de uso de transferência de SSL. Isso fornece uma perspectiva visual e lógica do link de confiança e a configuração entre o VPX e o dispositivo HSM.

<img src="images/network-flows-logical-topology.jpg" alt="drawing" style="width: 700px;"/>

Se você não estiver familiarizado com a transferência de SSL, revise este [artigo do Citrix](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html).

## O que você realizará

{: #what-you-ll-accomplish}

Neste guia passo a passo, você aprenderá a implementar e configurar um HSM com um {{site.data.keyword.vpx_full}}:

Tarefa  | Descrição
------------- | -------------
[Fazer o pedido de um Hardware Security Module (HSM)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) | Primeiro, você precisará pedir um HSM.
[Fazer o pedido de um {{site.data.keyword.vpx_full}}](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) | Se ainda não tiver pedido, você pedirá um {{site.data.keyword.vpx_full}}.
[Inicializar o HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) | A maioria das configurações requer a inicialização do dispositivo HSM. Sem isso, apenas determinados comandos `show` podem ser executados.
[Criar uma partição](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition) | Uma partição é um espaço lógico e independente que está associado ou conectado ao cliente que está solicitando ou criando objetos criptográficos no mecanismo do HSM.
[Instalar o software cliente do HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software) | Nesta subseção, o VPX será instalado com os softwares e utilitários necessários para interagir com o HSM. |
[Estabelecer o Network Trust Link (NTL)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) | Um Network Trust Link (NTL) é um canal seguro para o Hardware Security Module (HSM) e o cliente se comunicarem. |
[Criar chaves e gerar o Certificate Signing Request (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) | Nesta subseção, criaremos um par de chaves que será usado para gerar um Certificate Signing Request (CSR) e solicitar/pedir um certificado com ele. |
[Solicitar o certificado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) | Solicite um certificado SSL para o {{site.data.keyword.vpx_full}}.
[Recuperar e transferir o certificado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) | Recupere o certificado SSL pedido anteriormente e deixe tudo pronto para a sua instalação e configuração no próximo Passo a passo.
