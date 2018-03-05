---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Acessar e gerenciar o Citrix NetScaler VPX

Os dispositivos Citrix NetScaler são ferramentas poderosas com uma matriz de recursos que ajuda a aprimorar e refinar sua solução {{site.data.keyword.BluSoftlayer_notm}} em uma variedade de maneiras. É possível localizar informações do dispositivo no Portal do cliente, bem como se conectar ao dispositivo e configurar seus recursos.  

## Localizando detalhes do NetScaler no Portal do cliente

Os dispositivos Citrix NetScaler são listados na Lista de dispositivos como qualquer outro servidor que você tenha na Plataforma do {{site.data.keyword.BluSoftlayer_notm}}.

Para localizar a Lista de dispositivos:

1. Em seu navegador, abra [Portal do Cliente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window} e efetue login em sua conta.
2. Na navegação do Portal do cliente, selecione **Dispositivos > Lista de dispositivos**.

Você verá seus dispositivos, classificados por nome de dispositivo. Os dispositivos Citrix NetScaler VPX têm "NetScaler" como o Tipo de dispositivo. 

No lado esquerdo da linha para o NetScaler, clique na seta para expandir a linha e mostrar o Nome do usuário e uma senha mascarada para acesso de gerenciamento do NetScaler. 

Outros detalhes listados na Lista de dispositivos incluem: 

* Localização (do data center no qual o NetScaler reside)
* Endereço IP privado (usado para se conectar ao NetScaler para funções de gerenciamento)
* Data de início (quando a máquina foi pedida e provisionada)

**NOTA:** embora o endereço IP privado do NetScaler esteja listado no portal, o endereço IP público do NetScaler não está. Isso ocorre porque o gerenciamento do NetScaler é feito usando o endereço IP privado e os endereços IP públicos para dispositivos NetScaler são usados como o VIP ou IP virtual do dispositivo, que são usados para serviços de balanceamento de carga.

## A tela Detalhes do dispositivo 

Clicar no nome do NetScaler leva você para a página **Detalhes do dispositivo** do NetScaler, que mostra a VLAN na qual o NetScaler foi implementado, bem como seus endereços IP públicos para o NetScaler. Esses endereços IP não podem ser usados para gerenciamento, porque são os endereços VIP públicos padrão do NetScaler. Eles serão usados mais tarde para associação a um Serviço para propósitos de balanceamento de carga.

## Gerenciando o NetScaler

O {{site.data.keyword.BluSoftlayer_notm}} concede acesso raiz completo a seu dispositivo NetScaler. Para efetuar login na UI de gerenciamento do NetScaler, deve-se estar conectado à rede privada do {{site.data.keyword.BluSoftlayer_notm}} (VPN de gerenciamento do {{site.data.keyword.BluSoftlayer_notm}} ou executando funções de gerenciamento por meio de uma sessão remota em um servidor no ambiente do {{site.data.keyword.BluSoftlayer_notm}}). 

Para se conectar por meio do Portal do cliente à UI de Gerenciamento do NetScaler, clique na lista suspensa **Ações** no canto superior direito da tela **Detalhes do dispositivo** e escolha **Gerenciar dispositivo** para ativar uma nova guia ou janela pop-up em seu navegador. Isso o roteia ao NSIP do NetScaler (o endereço IP privado visto anteriormente). A página exibida solicita o nome do usuário raiz e a senha do dispositivo. Quando as informações forem inseridas, você será levado para a GUI de gerenciamento do NetScaler. 

Como alternativa, é possível copiar e colar o IP privado do dispositivo NetScaler em um navegador da web.

### Acesso ao NetScaler SSH

Também é possível se conectar ao dispositivo NetScaler diretamente usando seu cliente SSH favorito. Use o IP privado e as informações de login para o dispositivo NetScaler por meio da página Lista de dispositivos e certifique-se de que está conectado à VPN do {{site.data.keyword.BluSoftlayer_notm}}. 
