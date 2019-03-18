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

# Criar chaves e gerar o Certificate Signing Request (CSR)
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

Nesta subseção, criaremos um par de chaves que será usado para gerar um Certificate Signing Request (CSR) e solicitar/pedir um certificado com ele.

1.	Primeiro, confirme a lista de objetos no VPX. Use a senha especificada para essa partição durante a criação.

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	```

	Essa saída confirma que não existe objeto algum, pois a saída está em branco/vazia.

	Em seguida, verifique se a contagem de objetos é igual a 0 no HSM, exibindo os detalhes da partição:

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	Partition Name:                            partition6
	Partition SN:                              534071053
	Partition Label:                           partition6
	Partition Owner Locked Out:                no
	Partition Owner PIN To Be Changed:         no
	Partition Owner Login Attempts Left:       10 before Partition Owner is Locked Out
	Legacy Domain Has Been Set:                no
	Partition Storage Information (Bytes):     Total=207559, Used=0, Free=207559
	Partition Object Count:                    0

	Command Result : 0 (Success)
	```

	O comando listado acima usa a sintaxe abaixo:

	```
	partition show -p <partition_name>
	```

2.	Usando o Utilitário de Gerenciamento de Certificados (CMU) no VPX, crie um par de chaves por meio do comando mostrado abaixo. Mais uma vez, use a senha da partição designada.

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	Select RSA Mechanism Type -
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	Na sintaxe acima, o parâmetro `modulusBits` indica o comprimento em bits das chaves RSA,
enquanto `publicExponent` define o valor do expoente público a ser usado para a geração das chaves, isso deve ser configurado como 3, 17 ou 65537. A palavra-chave “etiqueta” é usada para especificar uma tag para que ela seja facilmente referenciada e identificada posteriormente. Para obter mais informações sobre os outros dois parâmetros ou parâmetros adicionais, verifique o [Guia de referência de utilitários
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Confirme se os objetos foram criados. No VPX:

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	No HSM:

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	Partition Name:                            partition6
	Partition SN:                              534071053
	Partition Label:                           partition6
	Partition Owner Locked Out:                no
	Partition Owner PIN To Be Changed:         no
	Partition Owner Login Attempts Left:       10 before Partition Owner is Locked Out
	Legacy Domain Has Been Set:                no
	Partition Storage Information (Bytes):     Total=207559, Used=1660,  Free=205899
	Partition Object Count:                    2

	Command Result : 0 (Success)
	```

4.	Usando as chaves criadas na etapa anterior, gere um CSR usando o utilitário CMU.

	Certifique-se de usar os valores corretos/apropriados para o Nome Comum (CN) e E-mail (E), o primeiro deve corresponder ao FQDN que será usado no registro DNS A associado ao Virtual Server/IP (VPX). O parâmetro E será usado para enviar os detalhes de aquisição de certificado após isso ser solicitado/pedido.

	```
	root@IBMADC690867-s6dr# cmu requestcertificate

	Please enter password for token in slot 0 : **********

	Enter Subject 2-letter Country Code (C) : US
	Enter Subject State or Province Name (S) : North Carolina
	Enter Subject Locality Name (L) : Durham
	Enter Subject Organization Name (O) : IBM
	Enter Subject Organization Unit Name (OU) : HSM
	Enter Subject Common Name (CN) : hsmclient7.projectgoldfinch.net   
	Enter EMAIL Address (E) : user@yourdomain.com
	Enter output filename : certreqnss6dr.csr
	```

	Na saída listada acima, o nome do arquivo pode ser qualquer coisa com uma extensão .csr, no entanto, uma descrição significativa é recomendada.

5.	Confirmar a criação do arquivo

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
