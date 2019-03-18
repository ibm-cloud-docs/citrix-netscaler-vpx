---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Implementação padrão do Citrix NetScaler VPX
{: #citrix-netscaler-vpx-default-deployment}

Ao visualizar o NetScaler em **Dispositivos > Lista de dispositivos** no [Portal do cliente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/), você poderá observar que ele parece diferente de outros servidores. Ou seja, o dispositivo tem um endereço IP privado, mas nenhum endereço IP público.

A implementação padrão de um NetScaler no {{site.data.keyword.BluSoftlayer_notm}} foi projetada para ser tão segura quanto possível, designando automaticamente um endereço IP privado como o NetScaler IP (NSIP) usado para propósitos de gerenciamento. Se você clicar na seta à esquerda do NetScaler, a linha será expandida para mostrar o nome de usuário padrão (raiz) e a senha mascarada do usuário raiz. 

O {{site.data.keyword.BluSoftlayer_notm}} manipula muitas das decisões para você durante o fornecimento. Por exemplo, quais endereços IP usar para quais propósitos. Ele pergunta quais VLANs você gostaria de usar para implementação. Além disso, ele automatiza boa parte da configuração de backend usando scripts e uma API, como designar interfaces a VLANs públicas e privadas separadas e designar os endereços IP adequados a cada interface, incluindo o NSIP, VIPs e SNIPs.

## O que eu preciso configurar?

Por padrão, o NSIP é o endereço IP privado designado durante o fornecimento, que é o endereço IP usado para se conectar ao NetScaler para propósitos de gerenciamento. Os SNIPs (Endereços SubNet IP), por padrão, são designados por meio dos mesmos SubNets de IP primário localizados nas VLANs escolhidas durante o processo de ordenação. 

Se você tiver escolhido as mesmas VLANs nas quais seus servidores de carga balanceada desejados residem, nenhuma configuração extra desses SNIPs será necessária. Por padrão, o DNS é configurado como os servidores de nomes do {{site.data.keyword.BluSoftlayer_notm}}. Em uma implementação básica, se o {{site.data.keyword.BluSoftlayer_notm}} hospedar os registros DNS para seus servidores, nenhuma configuração adicional será necessária.
