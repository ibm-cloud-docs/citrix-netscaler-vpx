---
copyright:
  years: 1994, 2018

lastupdated: "2018-06-28"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Fazer upgrade do Citrix NetScaler VPX

**NOTA:** deve-se estar conectado à VPN antes de tentar este procedimento.

1. Efetue login no IP de gerenciamento do NetScaler.
2. Clique em **Upgrade do sistema**.
4. Escolha **Local** na lista suspensa **Escolher arquivo**. 
4. Faça download do arquivo de upgrade correto no local a seguir:

	[Versões disponíveis do NetScaler ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}
	
	**OBSERVAÇÃO:** deve-se estar conectado à VPN da infraestrutura do IBM Cloud para acessar esse link.

5. Na tela Fazer upload de software, navegue para o local do arquivo de upgrade e clique em **Fazer upgrade**. O firmware será transferido por upload.
6. Na janela resultante Upgrade do sistema, a reinicialização será solicitada. Clique em **Fechar**.
7. Volte para **Sistema** e clique em **Reinicializar**.
8. Após o upgrade, feche todas as instâncias do navegador e limpe o cache do computador antes de acessar o dispositivo.

**OBSERVAÇÃO:** a interface com o usuário pode diferir dependendo da versão atual do NetScaler VPX.



