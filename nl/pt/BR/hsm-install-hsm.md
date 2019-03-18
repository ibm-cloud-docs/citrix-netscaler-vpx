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

# Instalar o software cliente do IBM Hardware Security Module (HSM)
{: #install-the-ibm-hardware-security-module-hsm-client-software}

Nesta etapa, o Citrix VPX será instalado com o software e os utilitários necessários para interagir com o HSM.

**NOTA:** as etapas um e dois neste procedimento são opcionais e serão necessárias apenas se o diretório safenet e os arquivos ou subpastas presentes nele estiverem ausentes do caminho `/var`. Esses recursos são necessários para o VPX a ser instalado com o software cliente e permitem que ele execute os utilitários associados ao software do HSM.

Localize as credenciais para acessar a CLI do NetScaler listada no Portal de Controle em **Dispositivos > Lista de dispositivos > Expandir nome do VPX**.

<img src="images/3-VPX-Credentials.png" alt="drawing" style="width: 400px;"/>

Elas serão necessárias para esta seção e o restante do guia.

**NOTA:** observe que todos os comandos e saídas do VPX neste documento listarão `netscalername#` (indicando uma execução de shell ou `>` (para a própria CLI do VPX).

1.	(OPCIONAL) Obtenha o arquivo `safenet_dirs.tar` e transfira-o para o VPX no diretório `/var`. O arquivo `safenet_dirs.tar` pode ser obtido [aqui ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://downloads.service.softlayer.com/citrix/netscaler/Safenet-HSM/){:new_window}.

	**NOTA:** deve-se estar com login efetuado na conta do SoftLayer para acessar o link acima.

	<img src="images/4-transfer-safenet_dirs.png" alt="drawing" style="width: 600px;"/>

	Esta imagem mostra o software WinSCP transferindo o arquivo `safenet_dir.tar` para o Citrix VPX.

2.	(OPCIONAL) Extraia o arquivo `tar`:

	```
	root@IBMADC690867-wnzs# tar -xvpf safenet_dirs.tar
	x safenet/
	x safenet/config/
	x safenet/gateway/
	x safenet/SAClient_600.tgz
	x safenet/SAClient_622.tgz
	x safenet/install_client.sh
	x safenet/gateway/start_safenet_gw
	x safenet/gateway/gw_delay
	x safenet/config/safenet_config
	x safenet/config/Chrystoki.conf
	```

3.	Navegue para o diretório `/var/safenet` e confirme se as pastas e arquivos foram transferidos:

	```
	extracted
	root@IBMADC690867-s6dr# cd safenet
	root@IBMADC690867-s6dr# pwd
	/var/safenet

	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        config                  install_client.sh
	SAClient_622.tgz        gateway
	```

4.	Execute o script de instalação usando a versão 622:

	```
	root@IBMADC690867-s6dr# install_client.sh -v 622
	*********************************************
	Current Version: 622
	Installing Version: 622
	Starting to extract SAClient_622.tgz file.
	Extracted SAClient_622.tgz file.
	Removing SAClient_622.tgz file.

	*********************************************

	Agora, siga o documento de etapas de configuração disponível on-line nos edocs do Citrix.
	*********************************************
	```

5.	Confirme a criação do diretório do safenet:

	```
	root@IBMADC690867-s6dr# ls
	SAClient_600.tgz        gateway                 installation.log
	config                  install_client.sh       safenet
	```

6.	Navegue para o diretório `/var/safenet/config/` e execute o script `safenet_config`:

	```
	root@IBMADC690867-s6dr# cd /var/safenet/config/
	root@IBMADC690867-s6dr# pwd               
	/var/safenet/config

	root@IBMADC690867-s6dr# sh safenet_config
	```

7.	Verifique se `/etc/Chrystoki.conf` e o link simbólico `/usr/lib/libCrystoki_64` foram criados:

	```
	root@IBMADC690867-s6dr# ls -l /etc/Chrystoki.conf
	-rw-r--r--  1 root  wheel  1185 Jul 26 16:17 /etc/Chrystoki.conf
	root@IBMADC690867-s6dr# ls -l /usr/lib/libCryptoki2_64.so
	lrwxr-xr-x  1 root  wheel  54 Jul 26 16:17 /usr/lib/libCryptoki2_64.so ->
	/var/safenet/safenet/lunaclient/lib/libCryptoki2_64.so
	```

O IBM© Hardware Security Module foi instalado com sucesso.
