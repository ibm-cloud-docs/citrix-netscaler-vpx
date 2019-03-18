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

# Inizializzazione di IBM Hardware Security Module (HSM)
{: #initialize-ibm-hardware-security-module-hsm-}

La maggior parte delle configurazioni richiede l'inizializzazione del dispositivo HSM. Senza eseguire tale operazione, possono essere eseguiti solo determinati comandi `show`.

Per inizializzare il tuo dispositivo, segui i passi riportati di seguito:

1.	Collegati utilizzando SSH al dispositivo IBM© Hardware Security Module con le credenziali elencate nel portale di controllo in **Devices > Device List > Expand HSM name**.

	In alternativa, puoi utilizzare l'autenticazione della chiave pubblica. Per ulteriori informazioni, consulta la [Appliance Administration Guide (pagina 38) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}.

	**NOTA:** generalmente, l'accesso SSH viene abilitato e consentito per impostazione predefinita. Se riscontri problemi nel collegarti con SSH, controlla la sicurezza e l'instradamento della tua infrastruttura.

2. Esegui il comando `hsm init`:

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

	Dove la sintassi utilizzata è: `hsm init -l <hsmlabel>`

Il parametro o l'etichetta `-l` è un parametro utilizzato per assegnare un identificativo all'HSM e può essere un testo o una descrizione significativi correlati all'azienda, all'amministratore o al ruolo che ricopre. La password dell'amministratore HSM sarà la password designata per il responsabile della sicurezza (Security Officer - SO) HSM ed è essenzialmente un profilo richiesto per creare e configurare oggetti di crittografia e per apportare modifiche all'ambiente HSM.

Infine, il dominio di clonazione è un identificativo condiviso che consente di formare gli oggetti tra un gruppo di HSM. Di norma viene utilizzato per backup e/o HA.

Consulta la [LunaSH Command Reference Guide ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window} per tutti i comandi disponibili supportati nella CLI HSM.
