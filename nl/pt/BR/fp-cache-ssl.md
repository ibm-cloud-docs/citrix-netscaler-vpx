---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, redirect, ssl, traffic

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

# Configurar o tráfego de Redirecionamento de cache para SSL (opcional)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

Em vez de definir o redirecionamento de cache para o servidor virtual com um protocolo HTTP ou HTTPS (conforme discutido na etapa anterior), talvez você queira defini-lo para manipular o tráfego SSL.

Para isso, siga estas etapas:

1. Acesse **Gerenciamento de tráfego > Redirecionamento de cache > Virtual Servers** e clique em **Incluir**. Especifique o nome para o servidor virtual de proxy de encaminhamento, selecione o protocolo SSL e um tipo de cache de **ENCAMINHAMENTO**. Designe a ele um endereço IP de sua sub-rede privada, com sua porta de requisito.

	<img src="images/fp14.png" alt="drawing" style="width: 300px;"/>

	Clique em **OK**.

2. Revise a página de resumo e clique em **OK** para continuar.
3. Especifique suas configurações de Redirecionamento, DNS Virtual Server e Destination Virtual Server.
4. Clique em **Certificado** no painel **Configurações avançadas** para visualizar a configuração relacionada ao certificado SSL.
5. Clique no campo vazio **Nenhum certificado do servidor**.
6. Na lista suspensa Selecionar certificado do servidor, selecione seu servidor SSL.
7. Insira as informações de configuração do certificado conforme necessário.

	<img src="images/fp15.png" alt="drawing" style="width: 400px;"/>

	Clique em **Instalar**.

8. Selecione **Ligar**.

	<img src="images/fp16.png" alt="drawing" style="width: 300px;"/>
