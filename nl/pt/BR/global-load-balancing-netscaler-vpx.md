---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Global Load Balancing com o Citrix NetScaler VPX
{: #global-load-balancing-with-citrix-netscaler-vpx}

O Global server load balancing (GSLB) é um mecanismo para distribuir o tráfego entre múltiplos servidores/instâncias, residindo geralmente em diferentes localizações geográficas. A ideia é ter um mecanismo/servidor de balanceamento global que receba solicitações de tráfego de clientes e as redirecione para uma determinada geografia, a última determinada usando os critérios/algoritmos selecionados e configurados pelo administrador. Para conseguir isso, dois métodos reconhecidos podem ser usados dentro da rede do {{site.data.keyword.BluSoftlayer_notm}}:

* **CDN:** Content Delivery Network (CDN) emitida para entregar conteúdo e rich media, como imagens e vídeos; a CDN distribui conteúdo geograficamente sobre os nós dispersos enquanto mantém a menor latência e as mais altas velocidades. Em geral ela é implementada quando partes específicas de conteúdo precisam ser distribuídas em vez de websites/aplicativos inteiros. O {{site.data.keyword.BluSoftlayer_notm}} oferece esse serviço; leia mais sobre ele [aqui](/docs/infrastructure/CDN?topic=CDN-getting-started). 
* **NetScaler VPX:** exatamente como o balanceamento de carga local regular, o VPX usa uma hierarquia de objeto semelhante para balancear a carga do tráfego entre várias geografias. Usando as consultas globais baseadas no DNS, o NetScaler escolhe o registro respectivo que corresponde ao local/site selecionado; a seleção baseia-se nos critérios pré-configurados pelo administrador. As seções recebidas serão expandidas nessa opção/oferta.

Observe que outras técnicas estão disponíveis para distribuição de conteúdo, como redirecionamento de HTTP, que também podem ser implementado com o Citrix NetScaler VPX. 

## Sobre o GSLB no VPX

O NetScaler VPX pode ser ativado com o GSLB simplesmente ativando seu recurso na CLI/GUI. 

O GSLB usa componentes/objetos muito semelhantes como aqueles usados em implementações de balanceamento de carga locais, nas quais entidades são definidas usando um modelo hierárquico.

O GSLB pode ser implementado para vários propósitos. Alguns deles poderiam ser:

* **Compartilhamento/distribuição de carga:** para distribuir recursos de maneira eficiente e inteligente entre múltiplas localizações.
* **Recuperação de desastre:** usada quando a localização principal ou primária fica inativa ou não consegue renderizar o serviço. Neste cenário uma localização alternativa/de backup pode assumir.
* **Desempenho/formato:** permite posicionar o conteúdo mais próximo de sistemas finais ou em uma maneira que aprimore o serviço em questão.

Os principais componentes ou entidades no processo/implementação de GSLB são:

* **Servidores virtuais:** um VIP é um endereço IP para o qual os clientes enviam solicitações, o NetScaler finaliza a conexão do cliente no VIP e, em seguida, inicia uma conexão com um servidor configurado no serviço de balanceamento de carga (local). 
* **DNS (Sistema de Nomes de Domínio) e servidores de nomes:** a resolução do nome no GSLB funciona de forma muito parecida ao DNS regular. A diferença é a lógica/critérios usados para determinar o endereço resolvido; o GSLB usa um método de balanceamento de carga pré-configurado para manipular essa resolução. O NetScaler pode ser configurado para interagir com o DNS em diferentes maneiras:
	* Authoritative DNS (ADNS). Os NetScalers que usam o modo ADNS têm autorização para um domínio específico e todos os seus registros.
	* Subdelegação de DNS. Ocorre quando um servidor DNS (autorizado do domínio) delega a responsabilidade de um subdomínio para um sistema NetScaler.
	* Proxy DNS. Quando configurado nesse modo, os NetScalers encaminham solicitações de DNS para outro servidor (externo) manipulando a resolução do nome.
* **Método:** o método é um algoritmo que o servidor virtual GSLB usa para selecionar o melhor serviço GSLB da topologia. O algoritmo avalia aspectos de desempenho que correspondem aos critérios de seleção reais. Os métodos a seguir estão disponíveis:
  * Round-robin: alterna solicitações recebidas para serem manipuladas entre os sites/serviços GSLB independentemente de sua carga.
  * Tempo de roundtrip (RTT): uma medida de tempo ou atraso entre o servidor DNS local do cliente e os sites (GSLB). O NetScaler usa mecanismos diferentes, como a solicitação/resposta de eco ICMP (PING), UDP e TCP, para reunir as métricas de RTT.
  * Proximidade estática: usa um banco de dados de endereço IP para estabelecer a proximidade entre o servidor DNS local do cliente e os sites e, em seguida, usa isso como critérios para fazer uma seleção.
  * Menos conexões: mede o menor número de conexões ativas em cada site/serviço como critérios de seleção.
  * Menor tempo de resposta: seleciona o site com o menor número de conexões ativas e o menor tempo médio de resposta.
  * Menos largura de banda: escolhe o site que está atualmente gerenciando a menor quantia de tráfego (Mbps).
  * Menos pacotes: seleciona o serviço que recebeu o menor número de pacotes nos últimos 14 segundos.
  * Hash de endereço IP de origem: faz uma seleção do serviço com base no valor de hash do endereço IPv4 ou IPv6 do cliente.
  * Carga customizada: seleciona um serviço que não está manipulando nenhuma transação ativa. Se todos os serviços na configuração de balanceamento de carga estiverem manipulando transações ativas, o dispositivo selecionará o serviço com a menor carga (uso de CPU, memória e tempo de resposta).

* **MEP (Metric Exchange Protocol):** um protocolo proprietário usado para trocar métricas (carga e rede) e informações de persistência entre os sites. O MEP fornece verificação de funcionamento entre os diferentes sites/NetScalers na engrenagem/topologia do GSLB. Usando os critérios configurados pelo administrador, o MEP fornece uma maneira para que os sites se comuniquem e manipulem o tráfego com base nos parâmetros de seleção configurados anteriormente. O MEP usa as portas TCP 3009 e 3011. Quando o MEP está desativado, a seleção de métodos fica limitada às opções listadas anteriormente, marcadas com um asterisco (*). Qualquer outro método escolhido poderia reverter para o Round-robin.
* **Monitoramento:** o mecanismo NetScaler avalia periodicamente o estado dos serviços GSLB remotos usando o MEP ou monitores explícitos ligados aos serviços em questão. Os monitores são usados exatamente como em um serviço de balanceamento de carga regular. No caso de GSLB, a inclusão de monitores em serviços locais não é necessária, pois o controle é feito geralmente pelo MEP. 
* **Persistência:** um recurso opcional que estabelece uma preferência do site por um domínio específico. Nesse caso de uso específico, o tráfego não tem a carga balanceada, mas manipulada pelo mesmo data center. Isso pode ser útil em alguns aplicativos, como e-commerce, em que os dados transacionais são exclusivos para cada site/servidor.
* **Site do GSLB:** os sites podem ser definidos como data centers ou locais nos quais um sistema NetScaler está configurado/presente. Cada site do GSLB é gerenciado por um sistema NetScaler que é considerado "local" para esse site, enquanto todos os outros sistemas/sites remotos são vistos e tratados como sites "remotos".
* **Serviço GSLB:** é um objeto que representa (e é ligado a) um servidor virtual/VIP (regular). Ele pode ser local (mesmo site) ou remoto.
* **Servidor virtual GSLB:** um servidor virtual GSLB é designado a um ou mais serviços GSLB que normalmente fariam parte de sites diferentes (GSLB). O tráfego recebido nele tem a carga balanceada entre os sites ligados a ele. A seleção do site é feita com base no método e no caso de uso.
* **Domínio GSLB:** representa o domínio ou a zona pela qual o servidor virtual GSLB é responsável. 
* **Serviço ADNS:** um serviço representado por uma combinação de endereço IP e porta; é onde as solicitações de DNS para um domínio para o qual o NetScaler tem autorização são enviadas. O NetScaler leva-as para o servidor virtual GSLB ligado a esse domínio para obter uma resposta.
