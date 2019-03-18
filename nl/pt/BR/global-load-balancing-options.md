---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Global Load Balancing
{: #global-load-balancing}

O Global server load balancing (GSLB) é um método para dividir o tráfego entre múltiplos servidores que usa DNS e localizações geográficas como o meio de determinar onde o tráfego do servidor deve ser enviado. Em geral, um balanceador de carga global envia uma solicitação do cliente para um servidor que está mais próximo do cliente, reduzindo a latência e melhorando o desempenho.

Talvez uma implementação completa de uma solução de balanceamento de carga global não seja necessária. O GSLB requer múltiplas instâncias de um dispositivo adequado que possa executar essa função e dependendo de suas necessidades, outras soluções podem ser mais atraentes para você. Se você precisar de websites e aplicativos inteiros, o GSLB é uma boa opção. Se precisar apenas de partes de seu conteúdo, como imagens, vídeos ou outros arquivos grandes, uma [Content Delivery Network](/docs/infrastructure/CDN?topic=CDN-about-content-delivery-networks-cdn-) poderá ser mais adequada (e mais fácil de implementar).

## Citrix NetScaler VPX

O Citrix NetScaler VPX é o único dispositivo configurável pelo cliente que executa o verdadeiro balanceamento de carga global. O NetScaler é um dispositivo multifuncional que pode executar consultas de balanceamento de carga global baseadas no DNS. É possível apontar para o NetScaler como um servidor DNS e o dispositivo verificará os servidores nos quais está configurado para balancear a carga, executará um cálculo de distância e retornará um registro com o IP do servidor mais próximo da solicitação do cliente.

Para balanceamento de carga global, você teria uma configuração do dispositivo NetScaler em cada data center. Cada configuração do dispositivo NetScaler pode ser um único Netscaler ou um par de Netscalers em um par de HA, dependendo de seus requisitos, fornecendo serviços de balanceamento de carga local para os servidores por trás deles. Os dispositivos são configurados para conversar entre si para que troquem informações de estado em cada servidor designado à rotação do balanceador de carga global. Qualquer solicitação de DNS que venha para esses NetScalers configurados pode retornar um registro adequado para um servidor que esteja on-line e seja responsivo. Qualquer servidor não responsivo é removido da rotação e outro é selecionado.

Deve-se já ter o balanceamento de carga configurado, mesmo se apenas um servidor estiver sendo balanceado. Você precisará de endereços IP adicionais para alguns serviços, isto é, o IP do site do GSLB. Esse IP é usado pelo NetScaler para se comunicar com os outros NetScalers no protocolo de balanceamento de carga global. 

O procedimento de balanceamento global a seguir usa:

### VPX1

`50.97.235.236` é denominado `VPX1Vserver` e é o VIP de balanceamento de carga local para esse dispositivo. `50.23.66.52` será denominado `VPX1site` e é o IP local para o GSLB desse dispositivo.

### VPX2
`208.43.241.249` é usado para `VPX2Vserver` e o IP do GSLB é `208.43.224.4`, denominado `VPX2site`.

1. Acesse **Gerenciamento de tráfego > GSLB** e clique com o botão direito para ativar o recurso. Em seguida, selecione **Sites** e **Incluir**.

2. No primeiro dispositivo, insira o Nome como VPX1, o Tipo como local e o IP como `50.23.66.52` e, em seguida, selecione **Fechar**. 

	Você deverá ver o site listado com um status de verde. Não inclua um site remoto ainda.

3. Acesse **Gerenciamento de tráfego > GSLB** e selecione o **Assistente do GSLB**. Clique em **Avançar**. Insira o nome do host que estará tendo a carga balanceada (neste exemplo, `gslb.tsstesting.com`). Deixe o Tipo de registro como A e o Tipo de serviço como QUALQUER UM. O nome do servidor virtual será preenchido sozinho. Clique em **Avançar**.

4. Escolha sua forma de método de balanceamento e persistência exatamente como faria com o balanceamento de carga regular. Clique em **Avançar**.

5. O site já está preenchido, portanto, não é necessário incluir nada. Em vez disso, clique no '+' verde próximo ao nome do primeiro site. Selecione o vserver nesse dispositivo na lista e clique em **Criar**. Você deverá ver que o site está configurado com o IP do site e o IP do vserver de sua configuração de carga balanceada e que é verde. Clique em **Avançar**, **Concluir** e **Sair**.

6. Execute as mesmas ações no próximo NetScaler usando os valores para esse servidor.

7. Em ambos os servidores, acesse **Gerenciamento de tráfego > DNS > Registros > Registros A** e examine a lista. Você deverá ver as entradas `root.servers.net` e também o seu nome de host, com um tipo de DOMÍNIO GSLB. 

8. Acesse **Gerenciamento de tráfego > DNS > Servidores de nomes** e clique em **Incluir**. Insira um endereço IP no NetScaler (como o IP público do dispositivo). Clique em **Local** e deixe o protocolo como UDP. Clique em **Criar** e, em seguida, em **Fechar**. Você deverá ver o estado efetivo como ativado e operacional.

9. Acesse **Sistema > Rede > IPs** e abra o endereço IP do GSLB. Certifique-se de que **Gerenciamento** esteja selecionado para ambas as máquinas.

10. Em seguida, em ambos os servidores, volte para **Gerenciamento de tráfego > GSLB** e passe pelo assistente novamente. Dessa vez, clique em **Avançar** e selecione **Modificar configuração para domínios existentes**. Selecione o nome do host na lista e, em seguida, clique em **Avançar** duas vezes. 

11. No campo de endereço do site, coloque o endereço IP do site do outro NetScaler e dê o nome do site do outro NetScaler a ele e clique em **Incluir**. O site será preenchido com uma opção para clicar no '+' verde novamente. Clique no sinal de mais do site remoto para incluir outro site. Insira o IP do serviço vserver (aquele para os servidores de carga balanceada, não o IP do site do GSLB) e a porta, clique em **Criar** e **Fechar**, **Avançar**, **Concluir** e, em seguida, **Sair**.

Se tudo estiver funcionando até este ponto e ambos os servidores estiverem configurados, tudo deverá ter um status de verde em Virtual Server, serviços e sites do GSLB. Você observará que agora haverá duas entradas nos serviços do GSLB em ambas as máquinas se elas estiverem sincronizadas corretamente. Neste ponto, os servidores estão agora se comunicando entre si.

Agora você precisa configurar o DNS.

Em nosso exemplo, `gslb.tsstesting.com`, você criaria registros cola e NS na zona tsstesting.com:

    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; nameserver IP of first NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; nameserver IP of second NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias to the GSLB object on the NetScaler appliance

Lembre-se, só é possível usar CNAMEs com nomes de host, não a raiz do domínio.

Essa configuração define os servidores de nomes para solicitações para `gslb.tsstesting.com` para os NetScaler IPs nos quais o DNS foi configurado. O registro CNAME converte `tsstesting.com` em uma solicitação para `gslb.tsstesting.com`. Quaisquer solicitações para `www.tsstesting.com` irão então para o NetScaler para serem resolvidas e retornarão um registro baseado no método de balanceamento de carga configurado.

Para obter mais informações sobre o balanceamento de carga global do NetScaler, consulte:
* [Configurando o Netscaler para balanceamento de carga global ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://support.citrix.com/article/CTX110348){: new_window}
* [Como o DNS (Sistema de Nomes de Domínio) funciona com o recurso GSLB no NetScaler ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.citrix.com/article/CTX122619){: new_window}
* [Informações sobre o protocolo MEP e o monitoramento do site ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://support.citrix.com/article/CTX111081){: new_window}

Há outros produtos que podem oferecer uma funcionalidade semelhante para difundir tráfego em uma base geográfica:

### CDN

As Redes de entrega de conteúdo (CDNs) permitem fazer upload ou fornecer um servidor de origem para servidores de cache geograficamente dispersos, que fornecem então o conteúdo para o cliente solicitante. As CDNs funcionam melhor com conteúdo em massa estático, como imagens e vídeos que não mudam ao longo do tempo.

Para obter mais detalhes sobre o CDN, consulte [esta documentação](/docs/infrastructure/CDN?topic=CDN-getting-started).

### Object Storage

O Object Storage do {{site.data.keyword.BluSoftlayer_notm}} pode ser configurado para usar múltiplas localizações geográficas em vários data centers para fornecer conteúdo. Um aplicativo geograficamente ciente pode executar consultas de localização na solicitação do cliente e retornar uma URL para o Object Storage que está próximo do cliente. O Object Storage também será fornecido com uma CDN de front-end, se necessário, para fornecer serviços adicionais de armazenamento em cache, conforme observado acima.

Para obter mais informações e uma introdução ao Object Storage, consulte [esta documentação](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-about-ibm-cloud-object-storage). 
