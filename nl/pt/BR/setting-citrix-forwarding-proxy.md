---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurar o Citrix Netscaler VPX como um proxy de encaminhamento

Um proxy de encaminhamento age como um único ponto de controle entre clientes em uma rede interna e a Internet. Um proxy permite que o Administrador de rede ou de segurança tenha a capacidade de criar políticas que restrinjam o acesso a sites da Internet.

Quando um cliente na rede interna iniciar uma solicitação, o endereço IP do proxy será usado para iniciar a solicitação para o servidor remoto na Internet. O servidor remoto, por sua vez, responderá de volta ao proxy, que retornará a resposta ao cliente.

Em geral, um proxy é combinado com um firewall para garantir a segurança de clientes em uma rede interna.

## Etapa 1: Solicitar VIPs a serem usados na Rede privada 

Quando um balanceador de carga Citrix NetScaler VPX é pedido no portal do cliente do {{site.data.keyword.BluSoftlayer_notm}}, supõe-se que um proxy reverso esteja sendo solicitado. O solicitante será solicitado a informar o número de IPs "públicos" a serem usados como IPs virtuais (VIPs).

No caso de um proxy de encaminhamento, os VIPs precisam ser configurados na rede privada. Um chamado de suporte precisa ser aberto para solicitar VIPs para a rede privada. O número de VIPs necessários determinará o tamanho da sub-rede solicitada no chamado. As informações de sub-rede serão retornadas no chamado.

Em nosso exemplo, solicitamos uma sub-rede `/29`, que resultou no seguinte:

* Criada a sub-rede `10.114.27.0/29` para uso como VIPs privados

* Subnet IP (SNIP) `10.114.52.101` e a sub-rede roteada `10.114.27.0/29`

* VIPs `10.114.27.0-3` foram incluídos no Citrix NetScaler VPX pela equipe de suporte

## Etapa 2: Ativar os recursos Balanceamento de carga e Redirecionamento de cache no Citrix NetScaler VPX

Por padrão, os recursos de balanceamento de carga e redirecionamento de cache no balanceador de carga Citrix NetScaler VPX ficam desativados; o comando `enable ns feature cr lb` ativa-os.


## Etapa 3: Criar o proxy de encaminhamento

Use a linha de comandos para emitir os comandos a seguir no Citrix NetScaler VPX. Em nosso cenário, somente um dos dois servidores DNS do {{site.data.keyword.BluSoftlayer_notm}} foi incluído.  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

A linha 1 cria o cache de redirecionamento. O protocolo é HTTP e `10.114.27.3` é um dos VIPs solicitados na rede privada. A porta é a porta padrão 80 para HTTP, mas como essa combinação de endereço e porta vai ser usada como a instrução de proxy no navegador, a porta poderá ser mudada para o que for necessário.

A linha 2 inclui um VIP de balanceamento de carga que representará o DNS "real".

A linha 3 inclui o endereço IP do DNS "real" como um serviço. Esse endereço pode ser o DNS do cliente ou roteado de volta para os resolvedores DNS fornecidos pelo {{site.data.keyword.BluSoftlayer_notm}}.

A linha 4 liga o VIP para o servidor "real". Todas as solicitações do DNS para `10.114.27.4` serão enviadas para `10.0.80.12`.

A linha 5 informa ao servidor virtual do proxy de encaminhamento para usar o DNS virtual para resolução do nome.

## Configurando o cliente

Antes de continuar a customizar o cliente para usar o proxy de encaminhamento, certifique-se de que não seja possível chegar a um site público (por exemplo, http://www.ibm.com) usando o navegador Firefox no cliente. Como não deve haver nenhuma interface pública no cliente, essa solicitação deve falhar. 

O exemplo a seguir configura um cliente Linux.

Algumas mudanças precisam ser feitas para o cliente. A primeira mudança é apontar o resolvedor no cliente para o DNS virtual, que pode ser feito de uma de duas maneiras.

É possível editar manualmente o `/etc/resolv.conf` para apontar para o endereço virtual do DNS. Esteja ciente de que as ferramentas de gerenciamento do cliente podem reverter essas mudanças para as configurações originais.  

Ou é possível editar a interface `/etc/sysconfig/network-scripts/ifcfg-ethx` e incluir a instrução `DNS1=`. Depois de configurado, o comando de reinicialização da rede de serviço pode ser emitido para assimilar as mudanças.

Em ambos os casos, o endereço IP do DNS precisará ser configurado como o endereço DNS virtual e o navegador do cliente precisará ser configurado para apontar solicitações para o proxy de encaminhamento do Citrix NetScaler VPX.

Use as etapas a seguir dentro do Firefox para fazer as mudanças necessárias:

1. Clique em **Preferências > Avançado > Rede > Configurações de conexão**.

* Selecione **Configuração manual de proxy** e insira o seguinte:

  * **Endereço:** 10.114.27.3

  * **Porta:** 80

  * Marque a caixa de seleção **Usar este servidor proxy para todos os protocolos**.

* Clique em **Salvar** e feche a janela do navegador.

O endereço IP `10.114.27.3` é o endereço IP do cache de encaminhamento criado na Etapa 1.

Neste ponto, a configuração está completa e é possível acessar a Internet por meio do recurso isolado na rede privada.

## Validando a configuração

Agora que o cliente está configurado para usar o proxy de encaminhamento, tente acessar um site público novamente. A solicitação deve agora ser bem-sucedida.

Os comandos de exibição a seguir podem ser usados para validar o estado do proxy de encaminhamento.

**show cr policy:** exibe todas as políticas existentes de redirecionamento de cache.

**show policy map:** exibe as políticas de mapa que foram configuradas e as informações de política de mapa relacionadas.

**show cr vserver:** exibe um servidor virtual de redirecionamento de cache especificado ou todos os servidores virtuais de redirecionamento de cache configurados.

**stat cr vserver:** exibe as estatísticas de redirecionamento de cache do vserver.

Acesse o [Guia de referência de comando do Citrix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.citrix.com/servlet/KbServlet/download/20679-102-665857/NS-CommandReference-Guide.pdf) para obter mais documentação.

A configuração de um proxy de encaminhamento básico no Citrix é bastante simples. Ela fornece uma maneira de dar aos clientes em uma rede interna um caminho seguro para os recursos na Internet. Ela também permite que o Administrador da rede mantenha um nível de controle na rede.

Se estiver implementando em um site do cliente, recomenda-se incluir um firewall na configuração para proteger ainda mais os recursos.
