---

copyright:
  years: 2018
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Implementando e configurando o IBM Hardware Security Module (HSM) com o Citrix Netscaler VPX
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

Este Passo a passo o guia ao longo do processo de integração do HSM com o Citrix Netscaler VPX. Os dois serviços serão, então, capazes de se comunicar e gerar o material criptográfico necessário para criar um certificado.

## Sobre a implementação
Esta implementação foi construída e testada com as seguintes especificações de componente:

| Versão e compilação do NetScaler VPX	| Versão do Software HSM | Versão do firmware do HSM | Versão do cliente do HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

**NOTA:** se você tiver uma versão mais antiga do VPX ou se, ao solicitar o dispositivo por meio da plataforma IBM© Cloud, somente vir versões 11.1 e anteriores como opções de seleção, o dispositivo poderá ser submetido a upgrade para que a configuração descrita neste guia possa ser concluída. 

## Topologia Lógica
O diagrama abaixo mostra o fluxo de tráfego de rede para o caso de uso de transferência de SSL. Isso fornece uma perspectiva visual e lógica do link de confiança e a configuração entre o VPX e o dispositivo HSM. 

<img src="images/network-flows-logical-topology.jpg" alt="drawing" style="width: 700px;"/>

Se você não estiver familiarizado com a transferência de SSL, revise este [artigo do Citrix](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html).

## O que você realizará

Neste guia passo a passo, você aprenderá a implementar e configurar um HSM com um Citrix Netscaler VPX:

Tarefa  | Descrição
------------- | -------------
[Fazer o pedido de um Hardware Security Module (HSM)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) | Primeiro, você precisará pedir um HSM.
[Fazer o pedido de um Citrix Netscaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) | Se ainda não tiver pedido, você pedirá um Citrix Netscaler VPX.
[Inicializar o HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) | A maioria das configurações requer a inicialização do dispositivo HSM. Sem isso, apenas determinados comandos `show` podem ser executados. 
[Criar uma partição](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition) | Uma partição é um espaço lógico e independente que está associado ou conectado ao cliente que está solicitando ou criando objetos criptográficos no mecanismo do HSM.
[Instalar o software cliente do HSM](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software) | Nesta subseção, o VPX será instalado com os softwares e utilitários necessários para interagir com o HSM. |
[Estabelecer o Network Trust Link (NTL)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) | Um Network Trust Link (NTL) é um canal seguro para o Hardware Security Module (HSM) e o cliente se comunicarem. |
[Criar chaves e gerar o Certificate Signing Request (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) | Nesta subseção, criaremos um par de chaves que será usado para gerar um Certificate Signing Request (CSR) e solicitar/pedir um certificado com ele. | 
[Solicitar o certificado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) | Solicite um certificado SSL para o Citrix Netscaler VPX.
[Recuperar e transferir o certificado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) | Recupere o certificado SSL pedido anteriormente e deixe tudo pronto para a sua instalação e configuração no próximo Passo a passo. 
