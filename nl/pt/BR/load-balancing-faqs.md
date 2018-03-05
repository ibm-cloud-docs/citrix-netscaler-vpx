---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

<a name="top"></a>
# Perguntas mais frequentes

A seguir estão as perguntas mais frequentes ao trabalhar com o Citrix NetScaler VPX.

## O que é Citrix NetScaler VPX?

O Citrix NetScaler é um controlador de entrega de aplicativo que torna os aplicativos cinco vezes melhor, acelerando o desempenho, assegurando a disponibilidade e proteção do aplicativo e reduzindo substancialmente os custos operacionais. Escolha a melhor edição do Citrix NetScaler que atenda aos requisitos de seu aplicativo e implemente-a no sistema dedicado apropriado para suas necessidades de desempenho. Para saber mais sobre o Citrix NetScaler, consulte a [página do NetScaler ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){: new_window}
no website do Citrix.

## Por que o balanceamento de carga é necessário?

O tráfego de balanceamento de carga tornou-se um aspecto importante de muitas implementações do cliente, pois distribui solicitações de aplicativo e cargas por múltiplos servidores. Ele também fornece vários benefícios para a topologia geral, incluindo:

* Segurança. O isolamento lógico dos servidores de aplicativos é criado ou as solicitações de tráfego são negadas com base em protocolos IP e números de portas.
* Alta disponibilidade. O conteúdo é replicado para um conjunto ou grupo de servidores, garantindo sua disponibilidade para hosts.
* Escalabilidade. É possível incluir servidores adicionais com o aumento da demanda, permitindo que o balanceador de carga distribua a carga de trabalho pelos servidores adicionais.
* Eficiência. As cargas de trabalho são distribuídas dinamicamente quando o balanceamento de carga é configurado. Por exemplo, recursos como CPUs podem ser usados de maneira mais eficiente.

## Quantas opções de balanceamento de carga estão disponíveis no {{site.data.keyword.BluSoftlayer_notm}}?

Para obter uma comparação detalhada das ofertas de Balanceador de carga da IBM, consulte [Explorar balanceadores de carga](https://dev-console.bluemix.net/docs/infrastructure/loadbalancer-service/explore-load-balancers.html#explore-load-balancers).

## O NetScaler suporta IPv6?

Sim. IPv6 e IPv4 são ambos suportados na rede pública do {{site.data.keyword.BluSoftlayer_notm}}.

## O balanceamento de carga do NetScaler trafegará na rede privada?

Sim, o NetScaler é o único produto de balanceamento de carga do {{site.data.keyword.BluSoftlayer_notm}} ampliado para a rede privada.

## O NetScaler pode ser configurado para relatar o endereço IP de origem do cliente em vez do IP de origem do dispositivo NetScaler?

Sim, o parâmetro **Use Source IP (USIP)** pode ser configurado como **YES** na Interface de gerenciamento avançada do NetScaler para permitir o relatório do IP de origem do cliente em vez daquele do NetScaler.

A ativação do modo de endereço USIP no dispositivo inclui flexibilidade no dispositivo para usar o endereço IP do cliente, disponível no cabeçalho IP, ao se comunicar com o servidor. Ao ativar esse modo, o dispositivo abre as conexões do servidor com o endereço IP do cliente e também fatora o endereço IP do cliente na reutilização da conexão. Portanto, esse modo facilita a reutilização limitada por cliente com base no endereço IP do cliente.

## Quais são as várias portas usadas para trocar as informações relacionadas a HA entre os nós em uma configuração de HA?

Porta 3010, para sincronização e propagação de comando. Porta UDP 3003, para trocar pacotes de pulsação.

## Qual versão do NetScaler VPX inclui o global server load balancing (GSLB)?

Platinum.

## Posso ter o NetScaler na configuração de HA?

Sim, os dispositivos NetScaler VPX suportam configurações de Alta disponibilidade (HA).

Os servidores NetScaler VPX não são redundantes, a menos que configurados no modo HA com um parceiro. Como parte de sua estratégia de backup e recuperação, é altamente recomendável implementar um ambiente de HA ao usar o NetScaler VPX.

Também é importante fornecer redundância para outros componentes de hardware e software. Por exemplo, fontes de alimentação e unidades de disco local podem não ter redundância. Uma falha nesses componentes pode resultar em perda de dados.

## A oferta {{site.data.keyword.BluSoftlayer_notm}} NetScaler inclui a funcionalidade SSL VPN?

Sim, esse recurso é conhecido como NetScaler Gateway™ e é incluído em todas as edições. Para obter mais informações sobre esse recurso, visite o [website do Citrix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.citrix.com/products/netscaler-adc/){: new_window}
