---



copyright:
  years: 2017
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configurar a NAT de origem para o tráfego de saída
{: #configure-source-nat-for-outbound-traffic}

A Conversão de Endereço de Rede (NAT) é um método de remapeamento de um espaço de endereço IP para outro, modificando as informações de endereço de rede no cabeçalho do IP dos pacotes enquanto eles estão em trânsito em um dispositivo de roteamento de tráfego.

É possível usar o dispositivo Citrix NetScaler VPX para executar a NAT no tráfego de saída das máquinas do cliente. Para isso:

1. Acesse Sistema > Rede > Rotas e navegue para a guia **RNAT**. Clique em **Configurar RNAT**.

2. Especifique a sub-rede (e máscara) de origem para as quais deseja aplicar RNAT e clique em **OK**.

O tráfego de ligação da Internet originado de qualquer IP nessa sub-rede usará agora NAT para trafegar no endereço IP público do Citrix NetScaler.    
