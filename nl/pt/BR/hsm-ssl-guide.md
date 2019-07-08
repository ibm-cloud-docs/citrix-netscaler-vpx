---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, configure, tune, tuning, ssl, offload

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

# Configurando e ajustando a transferência SSL com o Citrix Netscaler VPX
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

Este passo a passo fornece orientação sobre como configurar e ajustar a transferência SSL no Citrix Netscaler VPX. Isso é feito usando o certificado e o material criptográfico gerado por meio do link do HSM.

Este Passo a Passo considera que você concluiu as etapas em [Implementando e configurando o IBM© Hardware Security Module (HSM) com o Citrix Netscaler VPX](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) para solicitar e criar seu emparelhamento VPX/HSM.
{: note}

## Sobre a implementação
{: #about-the-deployment}
Esta implementação foi construída e testada com as seguintes especificações de componente:

| Versão e compilação do NetScaler VPX	| Versão do Software HSM | Versão do firmware do HSM | Versão do cliente do HSM |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## Topologia Lógica
{: #logical-topology}

O diagrama abaixo mostra o fluxo de tráfego de rede para o caso de uso de transferência de SSL. Isso fornece uma perspectiva visual e lógica do link de confiança e a configuração entre o Citrix VPX e o dispositivo HSM.

<img src="images/network-flows-logical-topology.jpg" alt="drawing" style="width: 700px;"/>

Se você não estiver familiarizado com a transferência de SSL, revise este [artigo do Citrix![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}.

## O que você realizará
{: #what-you-ll-accomplish}

Neste guia passo a passo, você aprenderá como configurar o SSL para um Citrix Netscaler VPX:

Tarefa  | Descrição
------------- | -------------
[Instalar o certificado](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) | Instale o certificado SSL que você criou no [Passo a passo](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) anterior.
[Verificar e configurar o registro DNS](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | Certifique-se de que exista um registro de DNS para o FQDN que aponte para o endereço público a ser configurado no Citrix Netscaler VPX como um Virtual Server.
[Incluir e configurar o SSL Virtual Server](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | Inclua e configure um SSL Virtual Server.
[Criar e aplicar um novo conjunto de cifras](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | Crie um conjunto de cifras que priorize e dê preferência ao AEAD, ao ECDHE e ao ECDSA.

## Recursos Adicionais
{: #additional-resources}
Os recursos adicionais a seguir podem ajudar você a obter o máximo do seu Citrix NetScaler VPX ao usar o IBM Hardware Security Module.

* [Documentação do produto NetScaler 12.1 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Portal de suporte da Gemalto ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [Suporte do IBM Cloud](/docs/get-support?topic=get-support-using-avatar){:new_window}
