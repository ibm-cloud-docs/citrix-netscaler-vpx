---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: upgrade, vpx, callhome

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Fazendo upgrade do seu {{site.data.keyword.vpx_full}}
{: #upgrading-your-citrix-netscaler-vpx}

Deve-se estar conectado à VPN antes de tentar realizar este procedimento.
{: note}

1. Efetue login no IP de gerenciamento do NetScaler.
2. Clique em **Upgrade do sistema**.
4. Escolha **Local** na lista suspensa **Escolher arquivo**.
4. Faça download do arquivo de upgrade correto no local a seguir:

	[Versões disponíveis do NetScaler ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}

	Deve-se estar conectado à VPN da Infraestrutura do IBM© Cloud para acessar este link.
  {: note}

5. Na tela Fazer upload de software, navegue para o local do arquivo de upgrade e clique em **Fazer upgrade**. O firmware será transferido por upload.
6. Na janela resultante Upgrade do sistema, a reinicialização será solicitada. Clique em **Fechar**.
7. Volte para **Sistema** e clique em **Reinicializar**.
8. Após o upgrade, feche todas as instâncias do navegador e limpe o cache do computador antes de acessar o dispositivo.


A interface com o usuário pode diferir dependendo da versão atual do seu NetScaler VPX.
{: note}

Se você estiver fazendo upgrade do NetScaler versão 11 para 12, o recurso CallHome será ativado por padrão, mesmo que você o desative especificamente antes e durante a instalação. Para desativar esse recurso, é possível usar a linha de comandos ou a UI de gerenciamento do Citrix:

   * Linha de comandos: `disable feature CallHome`
   * UI de gerenciamento do Citrix:

     1. Navegue para **Configuração** > **Sistema** > **Configurações**.
     2. Na área de janela de detalhes, clique no link **Configurar recursos avançados** e desmarque a opção **Callhome**.
     3. Clique em **OK**.
     {: note}
