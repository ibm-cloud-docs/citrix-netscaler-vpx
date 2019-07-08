---

copyright:
  years: 2019
lastupdated: "2019-04-28"

keywords: ipsec, vpn, vpx, tunnel

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

# Criando o roteamento baseado em política (PBR)
{: #creating-policy-based-routing}

Uma política de roteamento baseado em política (PBR) é necessária para especificar os parâmetros de tráfego exclusivos (como sub-redes locais e remotas) que a conexão VPN usará. Para criar um perfil PBR, execute as etapas a seguir:

1.	Navegue até **Sistema > Rede > PBR** e selecione **Incluir**.
2.	Insira o **Nome**.
3.	Mantenha **Ação** como a configuração padrão **ALLOW**.
4.	Para **Próximo tipo de hop**, selecione **Túnel de IP** e, em seguida, escolha o túnel [criado anteriormente](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-creating-ip-tunnel) na lista suspensa **Nome do túnel de IP**.
5.	Certifique-se de marcar **Ativar PBR**.
6.	Na seção **Configurar IP**, selecione **=** para o campo **Operação** para a origem e o destino.
7.	Especifique o primeiro e o último IP de sub-rede nos campos a seguir:
  *	**IP de origem baixo**
  *	**IP de origem alto**
  *	**IP de destino baixo**
  *	**IP de destino alto**
8.	Clique em **Criar**.

    <img src="images/ipseCreatePBR1.png" alt="desenho" style="width: 200px;"/>

9.	Em **Sistema > Rede > PBRs**, selecione o novo PBR, clique na lista **Selecionar ação** e, em seguida, escolha **Aplicar**.

    <img src="images/ipsecCreatePBR2.png" alt="desenho" style="width: 600px;"/>

Para criar o perfil PBR na CLI, use a sintaxe a seguir:

  ```
  > add ns pbr PBRforipsectunnel1 ALLOW -srcIP = 192.168.0.0-192.168.0.255 -destIP = 10.115.72.192-10.115.72.255 -ipTunnel
  IPSec_tunnel1 -priority 10
  > apply pbrs
  
  ```
  {: codeblock}

  Esteja ciente de que qualquer instância de servidor virtual ou infraestrutura destinada a passar pelo túnel VPN e ficar atrás do VPX precisará ser configurada para usar o VPX como o gateway padrão ou uma rota estática. Isso enviará o tráfego para o VPX quando o destino for a sub-rede remota (peer). Consulte o exemplo de rota estática (**10.115.0.0/16**) abaixo.
  {: note}

  ```
  >route print
  ===========================================================================
  Interface List
  3...06 93 7a 03 f0 b3 ......XenServer PV Network Device #0
  4...06 ff 8f 6d 89 e8 ......XenServer PV Network Device #1
  1...........................Software Loopback Interface 1
  7...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
  10...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
  ===========================================================================
  
  IPv4 Route Table
  ===========================================================================
  Active Routes:
  Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0    169.54.255.65    169.54.255.73     26
       10.115.0.0      255.255.0.0      192.168.0.1      192.168.0.2     26
  
  ```
  {: codeblock}
