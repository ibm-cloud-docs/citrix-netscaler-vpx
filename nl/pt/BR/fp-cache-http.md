---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, configure, configuration, http, traffic

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

# Configurar o tráfego de Redirecionamento de cache para HTTP(S)
{: #configure-cache-redirection-for-http-traffic}

Para configurar o tráfego de redirecionamento de cache para HTTP ou HTTPS, siga estas etapas:

1. Acesse **Gerenciamento de tráfego > Redirecionamento de cache > Virtual Servers** e clique em **Incluir**.
2. Especifique o nome de seu servidor virtual de proxy de encaminhamento. Selecione o protocolo **HTTP** e o tipo de cache **Encaminhamento** em suas respectivas listas suspensas. Em seguida, designe um endereço IP a esse servidor virtual por meio de sua sub-rede privada.

	<img src="images/fp12.png" alt="drawing" style="width: 300px;"/>

	Clique em **OK** para continuar.

3. Revise a página de resumo e clique em **OK**.  
4. Clique em **Configurações de tráfego** para visualizar definições de configuração adicionais.
5. Em Configurações de tráfego, selecione uma das três opções de redirecionamento a seguir, dependendo de seus requisitos:
	* **Cache** - Direciona todas as solicitações de saída para o conjunto de servidores de cache local.
	* **Política** - Verifica a política de redirecionamento de cache para determinar se a solicitação deve ser encaminhada para o conjunto de servidores de cache ou para os servidores de destino (origem).
	* **Origem** – Direciona todas as solicitações de saída para os respectivos servidores de destino (origem).

6. Na lista suspensa **Nome do DNS Virtual Server**, selecione o DNS Virtual Server configurado anteriormente e configure a opção **Redirecionar** como **Origem**.

	<img src="images/fp13.png" alt="drawing" style="width: 300px;"/>

	**NOTA:** a configuração do **Destination Virtual Server** é usada quando o tráfego de saída deve ser direcionado para o conjunto de servidores de cache local. Deixe-o vazio quando desejar direcionar todo o tráfego de saída para os servidores de origem.

7. Clique em **OK** e, depois, clique em **Pronto**.
