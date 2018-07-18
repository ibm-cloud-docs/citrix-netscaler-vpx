---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuração básica do balanceamento de carga
Considere uma empresa que tem um website básico de comunidade social no qual os usuários finais podem se registrar para uma conta que não requer informações confidenciais, após o qual o usuário pode efetuar login e postar fotos de seus animais. Há três servidores da web/aplicativos e um servidor de banco de dados para fazer backup deles. O domínio e o DNS estão hospedados com o {{site.data.keyword.BluSoftlayer_notm}} e como eles têm um ambiente pequeno, os servidores NetScaler e da web/app estão todos na mesma VLAN. Isso simplifica as coisas, pois nenhuma configuração adicional é necessária para que o NetScaler configure uma política básica de balanceamento de carga. O procedimento a seguir é uma explicação bem simplificada do fluxo de tráfego nesta instância:

1. Um usuário insere a URL em seu navegador.
2. O registro DNS da URL aponta para um dos VIPs públicos no NetScaler.
3. O NetScaler recebe o tráfego nesse VIP e anota o protocolo do tráfego que está sendo usado (tráfego da porta HTTP 80).
4. O NetScaler então transmite o tráfego para um dos servidores no conjunto de servidores, com base no método de balanceamento definido (round-robin, persistência de IP e assim por diante).
5. O servidor então aceita o tráfego, o usuário se conecta e efetua login.

Para realizar isso, o NetScaler precisaria ser configurado para manipular esse tráfego. Como o VIP, o IP do servidor DNS e o SNIP já estão configurados, isso simplifica a configuração. 

Na GUI do NetScaler, na tela Configuração, expanda **Gerenciamento de tráfego** no lado esquerdo. Expanda a subseção intitulada **Balanceamento de carga**. Em seguida, informe ao NetScaler quais servidores de destino serão incluídos na política de balanceamento de carga, seguindo este procedimento:

1. Em Balanceamento de carga, clique em **Servidores**.
2. Clique em **Incluir**.
3. Insira o Nome do servidor (por exemplo, Web1).
4. Insira o endereço IP do servidor.
5. Deixe o campo **Domínio de tráfego** em branco, pois você só está preocupado em usar o domínio de tráfego padrão neste cenário.
6. Insira os comentários desejados sobre esse servidor.
7. Clique em **Criar**.

Repita este procedimento para todos os servidores no conjunto.  

**DICA:** para manter os servidores facilmente identificáveis, use uma convenção de nomenclatura semelhante para servidores dentro do mesmo conjunto (por exemplo, Web1, Web2, Web3 e assim por diante).

Em seguida, crie seus Serviços. Você estará criando um Serviço para cada Servidor recém-inserido. O Serviço é o que configura a conexão entre o NetScaler e os servidores no conjunto. Cada serviço tem um nome e especifica um endereço IP, uma porta e o tipo de dados servido.

1. Clique em **Gerenciamento de tráfego > Balanceamento de carga > Serviços**.
2. Clique em **Incluir**.
3. Crie um serviço para cada servidor criado anteriormente, utilizando as mesmas informações.

Em seguida, crie um Virtual Server. O Virtual Server é uma espécie de conexão virtual entre o VIP usado para servidores de carga balanceada e serviços criados anteriormente.

1. Clique em **Gerenciamento de tráfego > Balanceamento de carga > Virtual Servers**.
2. Clique em **Incluir**.
3. Dê um nome ao Virtual Server.
4. Designe o protocolo que estará sendo balanceado (HTTP).
5. Deixe o Tipo de endereço IP como o padrão (Endereço IP). O campo de endereço IP é onde você inserirá o VIP que estará sendo usado como o ponto de entrada para todos os seus usuários.
6. Designe a porta. O padrão é a porta 80.
7. Clique em **OK**.

Agora, ligue os serviços criados para seu Virtual Server.

1. Na tela Virtual Servers, clique no link **Nenhuma ligação de serviço do Virtual Server de balanceamento de carga**.
2. Ligue cada um dos Serviços criados anteriormente ao Virtual Server.
3. Clique em **Pronto**.
4. Clique no botão **Atualizar**. O Estado e o Estado efetivo serão mostrados como verde.

Você criou um conjunto e uma política de balanceamento de carga para seu website.

**OBSERVAÇÃO:** para saber mais sobre a configuração do dispositivo Citrix NetScaler VPX, visite a [página de documentação do Citrix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/netscaler.html). Para obter assistência adicional, entre em contato com o suporte e vendas do {{site.data.keyword.BluSoftlayer_notm}}.
