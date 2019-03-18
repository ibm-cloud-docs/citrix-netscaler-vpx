---

copyright:
  years: 2018
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Incluir e configurar o SSL Virtual Server
{: #add-and-configure-the-ssl-virtual-server}

Para incluir e configurar o SSL Virtual Server, execute o procedimento a seguir:

1. Navegue para **Sistema > Configurações > Configurar recursos básicos**. Selecione **Transferência SSL** e, em seguida, clique em **OK**.
2. Na GUI do NetScaler, navegue para **Gerenciamento de tráfego > Balanceamento de carga > Serviços > Incluir** e especifique o nome, o endereço IP e configure o protocolo como **HTTP**. Pressione **OK** para concluir.
3. Confirme se o serviço está operacional:

	<img src="images/15-confirm-service.png" alt="drawing" style="width: 700px;"/>

4. Repita a etapa dois para quaisquer servidores adicionais.
5. Navegue para **Gerenciamento de tráfego > Balanceamento de carga > Virtual Servers >** e clique em **Incluir**. Especifique o nome e o selecione **SSL** como o Protocolo e, em seguida, insira o endereço IP público. Pressione **OK** para concluir.
6. Agora, selecione **Nenhuma ligação de serviços do servidor virtual de balanceamento de carga** e clique em **Selecionar**. Selecione o serviço ou serviços criados nas etapas anteriores e clique em Selecionar, em seguida, clique em **Ligar/Continuar**.

	<img src="images/18-bind-service.png" alt="drawing" style="width: 700px;"/>

7. Finalmente, clique em **Nenhum certificado do servidor** e, em seguida, clique em **Selecionar certificado do servidor** e selecione o certificado instalado anteriormente. Clique em **Selecionar**, em seguida, em **Ligar/Continuar**, em seguida, em **Pronto** para concluir.
