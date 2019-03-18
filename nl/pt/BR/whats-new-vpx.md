---
copyright:
  years: 1994, 2018
  
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Atualizações recentes para o Citrix NetScaler VPX
{: #recent-updates-for-citrix-netscaler-vpx}

## Versão 12.1

### Servidores virtuais com vários endereços IP
Agora é possível criar um único servidor virtual de balanceamento de carga com múltiplos endereços IPv4 e IPv6 VIP não consecutivos/consecutivos. Cada endereço VIP ligado a um servidor virtual é tratado como um servidor virtual individual.

Para obter mais informações sobre esse recurso, consulte o artigo Citrix [Diversos servidores virtuais do IP
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}.

### SSL
As atualizações a seguir foram aplicadas para conexões SSL:
 
* Remoção de cifras fracas do grupo de cifras DEFAULT_BACKEND. 
* Suporte para cifras ECDHE no frontend do HSM externo do Thales nShield®
* Suporte para cifras ECDHE no frontend do HSM externo de rede SafeNet
* Remoção do SSLv2: o dispositivo NetScaler VPX não suporta SSLv2 a partir da liberação 12.1.

Para obter mais detalhes sobre as atualizações SSL da versão 12.1, consulte [Notas sobre a liberação do Citrix 12.1
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}.

### Suporte a grupos de serviços para GSLB
Agora é possível configurar grupos de serviços baseados em endereço IP, grupos de serviços baseados em nome de domínio ou grupos de serviços de escala automática baseada em nome de domínio para GSLB. Também é possível gerenciar um grupo de serviços com a mesma facilidade de um único serviço e vincular um grupo de serviços a um servidor virtual, além de incluir serviços no grupo.

Para obter mais informações sobre os grupos de serviço GSLB, consulte o artigo do Citrix [Configurando um grupo de serviços GSLB![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}.
