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

# Configurar o DNS Virtual Server
{: #configure-the-dns-virtual-server}

Para configurar um DNS Virtual Server:

1. Acesse Gerenciamento de tráfego > Balanceamento de carga > Servidores. 
2. Clique em Incluir para incluir os dois resolvedores DNS do IBM© Softlayer: o 10.0.80.11 e o 10.0.80.12. 

	<img src="images/fp5.png" alt="drawing" style="width: 200px;"/> <img src="images/fp5b.png" alt="drawing" style="width: 200px;"/>

3. Em seguida, crie e defina seu Grupo de Serviços DNS, acessando Gerenciamento de tráfego > Balanceamento de carga > Grupos de serviços e selecionando Incluir. 

	<img src="images/fp6.png" alt="drawing" style="width: 400px;"/> 

4. Selecione o protocolo DNS e, em seguida, clique em OK.

	<img src="images/fp7.png" alt="drawing" style="width: 300px;"/> 
	
5. Na próxima tela, inclua os novos resolvedores de DNS como servidores membros neste grupo de serviços DNS, clicando primeiro no campo vazio em **Membros do grupo de serviços**. 

6. No painel Criar membro do grupo de serviços, especifique a porta DNS 53, em seguida, clique em Criar. 

	<img src="images/fp8.png" alt="drawing" style="width: 200px;"/> 
	
7. Clique em Fechar e, em seguida, clique em Pronto. 

	Assumindo que os dois resolvedores DNS do IBM Softlayer podem ser acessados do seu dispositivo Citrix NetScaler VPX, o grupo de serviços será mostrado como verde. 

8. Agora, acesse Gerenciamento de tráfego > Balanceamento de carga > Virtual Servers e clique em Incluir para definir seu DNS Virtual Server.
9. Em Configurações básicas, forneça um nome para seu servidor virtual, escolha o protocolo DNS e a porta 53, em seguida, designe um endereço IP de sua sub-rede privada. 

	<img src="images/fp9.png" alt="drawing" style="width: 300px;"/> 
	
10. Na página a seguir, clique no campo vazio rotulado **Nenhuma ligação do grupo de serviços do servidor virtual de balanceamento de carga**.
11. Selecione seu grupo de serviços DNS definido anteriormente na lista suspensa e clique em Ligar.  

	<img src="images/fp10.png" alt="drawing" style="width: 300px;"/> 
	
12. Clique em Continuar, depois, clique em Pronto. 

O estado do DNS Virtual Server agora deve ser mostrado como verde. 

<img src="images/fp11.png" alt="drawing" style="width: 500px;"/> 
