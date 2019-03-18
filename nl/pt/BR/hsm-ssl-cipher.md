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

# Criar e aplicar um novo conjunto de cifras
{: #create-and-apply-a-new-cipher-suite}

Um conjunto de cifras é uma combinação de autenticação, criptografia, Código de Autenticação de Mensagem (MAC) e algoritmos de troca de chave usados para negociar as configurações de segurança para protocolos SSL e TLS.

Para garantir a autenticação adequada, deve-se assegurar que o Citrix Netscaler VPX use a melhor combinação de cifras.

Para saber mais sobre os conjuntos de cifras SSL e outras melhores práticas, visite os links a seguir:

* [Conseguindo uma nota A+ em SSLlabs.com com o Citrix NetScaler ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.citrix.com/blogs/2018/05/16/scoring-an-a-at-ssllabs-com-with-citrix-netscaler-q2-2018-update/){:new_window} – atualização do 2º trimestre de 2018 (consulte as etapas três e cinco no guia de comando)
* [Melhores práticas de implementação de SSL e TLS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices#23-use-secure-cipher-suites){:new_window}
* [Como configurar o ECC no NetScaler? ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.citrix.com/article/CTX205289){:new_window}

**NOTA:** este tópico se concentra em configurações específicas e necessárias para as cifras SSL. As informações nos links anteriores podem fornecer configurações adicionais que podem ser aplicadas para otimizar a operação de SSL.

Para criar um novo conjunto de cifras que priorize as cifras AEAD, ECDHE e ECDSA, execute o procedimento a seguir:

1.	Insira os comandos a seguir simultaneamente em sua CLI do Citrix VPX e assegure-se de que sejam todos aplicados:

	```
	add ssl cipher SSLLABS
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-256-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-256-CBC-SHA
	```

	A sintaxe para os comandos anteriores é a seguinte:

	```
	add ssl cipher <cipherGroupName>
	bind ssl cipher <cipherGroupName> -cipherName <string>
	```

2.	Confirme se a cifra foi incluída em seu Citrix Netscaler VPX:

	```
	> show ssl cipher SSLLABS
	1)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256       Priority : 1
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02b
	2)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384       Priority : 2
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc02c
	3)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES128-SHA256   Priority : 3
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA-256   HexCode=0xc023
	4)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES256-SHA384   Priority : 4
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA-384   HexCode=0xc024
	5)      Cipher Name: TLS1-ECDHE-ECDSA-AES128-SHA        Priority : 5
	        Description: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA1   HexCode=0xc009
	6)      Cipher Name: TLS1-ECDHE-ECDSA-AES256-SHA        Priority : 6
	        Description: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA1   HexCode=0xc00a
	7)      Cipher Name: TLS1.2-ECDHE-RSA-AES128-GCM-SHA256 Priority : 7
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02f
	8)      Cipher Name: TLS1.2-ECDHE-RSA-AES256-GCM-SHA384 Priority : 8
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc030
	9)      Cipher Name: TLS1.2-ECDHE-RSA-AES-128-SHA256    Priority : 9
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA-256   HexCode=0xc027
	10)     Cipher Name: TLS1.2-ECDHE-RSA-AES-256-SHA384    Priority : 10
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA-384   HexCode=0xc028
	11)     Cipher Name: TLS1-ECDHE-RSA-AES128-SHA  Priority : 11
	        Description: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0xc013
	12)     Cipher Name: TLS1-ECDHE-RSA-AES256-SHA  Priority : 12
	        Description: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0xc014
	13)     Cipher Name: TLS1.2-DHE-RSA-AES128-GCM-SHA256   Priority : 13
	        Description: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0x009e
	14)     Cipher Name: TLS1.2-DHE-RSA-AES256-GCM-SHA384   Priority : 14
	        Description: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0x009f
	15)     Cipher Name: TLS1-DHE-RSA-AES-128-CBC-SHA       Priority : 15
	        Description: SSLv3 Kx=DH       Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x0033
	16)     Cipher Name: TLS1-DHE-RSA-AES-256-CBC-SHA       Priority : 16
	        Description: SSLv3 Kx=DH       Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0039
	17)     Cipher Name: TLS1-AES-128-CBC-SHA       Priority : 17
	        Description: SSLv3 Kx=RSA      Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x002f
	18)     Cipher Name: TLS1-AES-256-CBC-SHA       Priority : 18
	        Description: SSLv3 Kx=RSA      Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0035
 	Done
 	```

3. Desvincule o conjunto de cifras padrão de seu servidor virtual e ligue ao grupo customizado criado na etapa anterior:

	```
	unbind ssl vserver https_vip2 -cipherName DEFAULT

	bind ssl vserver https_vip2 -cipherName SSLLABS

	bind ssl vserver https_vip2 -eccCurveName ALL
	```

	A sintaxe para os comandos anteriores é:

	```
	unbind ssl cipher <cipherGroupName> -cipherName <string>
	bind ssl vserver <vServerName> -cipherName <string>
	bind ssl vserver <vServerName> -eccCurveName <eccCurveName>
	```

4.	Confirme as mudanças em seu servidor virtual:

	```
	> show ssl vserver https_vip2

	[OUTPUT OMITTED]
		ECC Curve: P_256, P_384, P_224, P_521

	1)      CertKey Name: hsmclient7ns      Server Certificate

	1)      Cipher Name: SSLLABS
		Description: User Created Cipher Group
 	Done
	```

5. (OPCIONAL) O redirecionamento de HTTP pode ser ativado para redirecionar usuários para um website seguro quando eles criam uma solicitação de HTTP (em oposição a HTTPS).

	Consulte [Como configurar o redirecionamento HTTP para HTTPS no NetScaler ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.citrix.com/article/CTX201201){:new_window} para obter instruções de configuração.
6. Teste a conexão HTTPS abrindo um navegador da web e inserindo o FQDN. O site deve carregar o conteúdo renderizado pelo serviço HTTP por trás do Citrix VPX.

	Também é possível visualizar os detalhes do certificado clicando no ícone de cadeado próximo à URL em seu navegador para exibir as informações de certificado.

	<img src="images/21-check-certificate.png" alt="desenho" style="width: 350px;"/>

	Se o redirecionamento foi configurado na etapa cinco, o site seguro também será carregado ao usar uma solicitação de HTTP.
