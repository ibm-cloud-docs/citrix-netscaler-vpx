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

# Verificar e configurar o registro DNS
{: #check-and-configure-the-dns-record}

Neste exemplo de Passo a passo, o serviço DNS do IBM© Cloud Internet Services é usado para gerenciar a zona DNS e seus registros. Nesse caso, deve-se assegurar que um registro seja criado para que o FQDN seja usado. O registro deve apontar para o endereço público a ser configurado no servidor virtual do Citrix Netscaler VPX.

<img src="images/12-add-record.png" alt="drawing" style="width: 700px;"/>

O IP público estático a ser usado com o Citrix VPX pode ser recuperado no Portal do Cliente, navegando para **Dispositivos > Lista de dispositivos** e, em seguida, selecionando o nome do Citrix Netscaler VPX.

<img src="images/13-check-ip.png" alt="drawing" style="width: 300px;"/>
