---
copyright:
  years: 1994, 2018

lastupdated: "2018-06-28"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurar o Citrix Netscaler VPX para Alta disponibilidade (HA)

Os balanceadores de carga são usados para balancear o tráfego em múltiplos servidores de aplicativos para melhorar o desempenho e a estabilidade em um aplicativo escalável. No entanto, um único balanceador de carga é um ponto único de falha. Evite isso configurando um par de Netscaler VPX de Alta disponibilidade (HA). A configuração de um par HA requer dois servidores Netscaler VPX. O servidor secundário continuará o balanceamento de carga se o principal falhar. 

O SNIP (SubNet IP) é o IP visto pelos servidores de carga balanceada como o IP de origem das solicitações (conexões) feitas no VIP (IP virtual) do Netscaler VPX. Normalmente, em uma configuração de par HA, o SNIP não muda, mas é possível que ele faça isso durante um evento de failover. Quando os dois Netscalers estão na mesma sub-rede, é possível que o SNIP do Netscaler VPX secundário mude para o SNIP usado originalmente pelo Netscaler VPX primário. Isso não causará nenhuma confusão para os servidores que manipulam a solicitação.

Para uma configuração de HA, ambos os NetScalers devem estar na mesma VLAN e na mesma sub-rede.

Antes de iniciar a configuração de HA, assegure-se de executar as ações de pré-requisito a seguir:

1. Se o par for configurado como ativo/ativo, quaisquer sub-redes VIP incluídas nas instâncias deverão ser do tipo "Roteadas para a VLAN".
* Se o par for configurado como ativo/passivo, quaisquer sub-redes VIP incluídas nas instâncias deverão ser "Roteadas para a VLAN" ou "Secundário roteado para IP" e roteado para o endereço IP público do nó primário.

Depois de ordenar os dois servidores Netscaler VPX na VLAN necessária e de ordenar as sub-redes VIP e SNIP para atender aos pré-requisitos de sua configuração do par HA, será possível continuar com o seguinte:

1. Abra duas janelas do navegador e efetue login na interface avançada em ambos os NetScalers. No NetScaler secundário, acesse **Sistema > Administração do usuário > Usuários** e configure a senha raiz como a mesma senha do NetScaler primário. Em seguida, atualize a senha no arquivo no portal do {{site.data.keyword.BluSoftlayer_notm}} na página de detalhes do dispositivo para corresponder à senha configurada para o secundário.

2. No VPX que você deseja que seja secundário, clique em **Sistema > Alta disponibilidade** e, em seguida, clique com o botão direito na primeira linha e clique em **Editar**. Selecione **Permanecer secundário** na caixa suspensa de configuração Status de alta disponibilidade e clique em **OK**.

3. Selecione **Incluir**. Insira o endereço IP do sistema do outro VPX (isso está localizado na guia Alta disponibilidade no primário) e insira os detalhes do login raiz na parte inferior. Deixe a caixa **Ativar INC** desmarcada. Clique em **OK**. 
	
	Se você recebe um erro alegando que os IPs não estão na mesma sub-rede, é possível que ambos os servidores VPX não estejam na mesma VLAN. Caso contrário, você deverá agora ser capaz de abrir o servidor principal e selecionar o botão **Atualizar** para ver ambos os servidores operando em Alta disponibilidade. 

	O novo IP de gerenciamento do NetScaler para o secundário será um endereço IP inferior ao anterior. Se não for possível obter nenhum acesso ao VPX secundário, remova a alta disponibilidade da linha de comandos usando:

	`sh ha node`

	Em seguida, remova o que seria o nó ha:
	
	`rm ha node 1`

4. No VPX primário você deve ver que o VPX remoto está agora sendo sincronizado. Acesse o servidor secundário e verifique a configuração **Rede > IPs**. Você deverá ver o VIP do servidor principal e outros IPs listados como passivos.

6. Retorne para **Sistema > Alta disponibilidade** no servidor secundário e clique em **Editar**. Selecione **ATIVADO** na caixa suspensa e pressione **OK**.

7. Force um teste de failover. Atualize a tela e observe os endereços IP se tornarem ativos no secundário. Efetue failover novamente e observe se tornarem passivos. Execute ping dos IPs para certificar-se de que funcionem.

8. O servidor principal deverá agora ser rotulado como primário e o secundário, caso o relatório tenha um estado de sincronização de sucesso.
