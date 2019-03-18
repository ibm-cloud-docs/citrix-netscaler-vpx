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

# Recuperar e transferir o certificado
{: #retrieve-and-transfer-the-certificate}

Recupere o certificado SSL solicitado anteriormente para que você esteja pronto para sua instalação e configuração no próximo Passo a passo, [Configurando e ajustando a transferência SSL com o Citrix Netscaler VPX ](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx).

1. Logo após validar a propriedade do domínio, você deverá receber um e-mail confirmando a conclusão do cumprimento do certificado e o próprio certificado.

	Copie o texto de `---BEGIN CERTIFICATE---` até `---END CERTIFICATE---` e salve o conteúdo como um novo arquivo de certificado com uma extensão de `.cer`.

2. Copie o arquivo de certificado para o diretório `/nsconfig/ssl` no Citrix Netscaler VPX.

<img src="images/11-transfer-certificate.png" alt="drawing" style="width: 600px;"/>

O Citrix Netscaler VPX agora está pronto para incorporar o certificado em uma implementação de balanceamento de carga usando SSL.
