---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, initialize

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

# Inicializar o IBM Hardware Security Module (HSM)
{: #initialize-ibm-hardware-security-module-hsm-}

A maioria das configurações requer a inicialização do dispositivo HSM. Sem isso, apenas determinados comandos `show` podem ser executados.

Para inicializar seu dispositivo, siga as etapas abaixo:

1.	Conecte-se usando o SSH no dispositivo IBM© Hardware Security Module com as credenciais listadas no Portal de Controle em **Dispositivos > Lista de dispositivos > Expandir o nome do HSM**.

	Como alternativa, é possível usar a autenticação de chave pública. Para obter mais informações, revise o [Guia de Administração do Dispositivo (página 38) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}.

	O acesso SSH é geralmente ativado e permitido por padrão. Se você tiver problemas ao se conectar com o SSH, verifique o roteamento e a segurança da infraestrutura.
  {: note}

2. Execute o comando `hsm init`:

	```
	[jpmongehsm2] lunash:>hsm init -l jpmonge

	Please enter a password for the HSM Administrator:
	> ********

	Please re-enter password to confirm:
	> ********

	Please enter a cloning domain to use for initializing this HSM:
	> ********

	Please re-enter cloning domain to confirm:
	> ********

	CAUTION:  Are you sure you wish to initialize this HSM?

	Type 'proceed' to initialize the HSM, or 'quit'
		to quit now.
		> proceed
		'hsm init' successful.

	Command Result : 0 (Success)
  	```

	Em que a sintaxe usada é: `hsm init -l <hsmlabel>`

O parâmetro ou etiqueta `-l` é um parâmetro usado para designar um identificador para o HSM e pode ser qualquer texto significativo ou descrição relacionada ao negócio, ao administrador ou à função que ele desempenha. A senha do administrador do HSM será a senha designada para o Responsável pela segurança (SO) do HSM, e é essencialmente um perfil necessário para criar e configurar objetos criptografados, assim como fazer mudanças no ambiente do HSM.

Por último, o domínio de clonagem é um identificador compartilhado que permite que os objetos sejam formados entre um grupo de HSMs. Isso é geralmente usado para backup e/ou HA.

Consulte o [Guia de Referência de Comando do LunaSH![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window} para todos os comandos disponíveis suportados na CLI do HSM.
