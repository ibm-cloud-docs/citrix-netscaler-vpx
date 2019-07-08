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

# Upgrade del tuo Citrix NetScaler VPX
{: #upgrading-your-citrix-netscaler-vpx}

Devi essere connesso alla VPN prima di tentare questa procedura.
{: note}

1. Accedi nell'IP di gestione NetScaler.
2. Fai clic su **System Upgrade**.
4. Scegli **Local** dall'elenco a discesa **Choose File**.
4. Scarica il file di upgrade corretto dalla seguente ubicazione:

	[VersiNetScaler Available Versions ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}

	Devi essere connesso alla VPN dell'infrastruttura IBM© Cloud per poter accedere a questo link.
  {: note}

5. Nella schermata Upload Software, individua l'ubicazione del file di upgrade e fai clic su **Upgrade**. Sarà caricato il firmware.
6. Nella finestra System Upgrade risultante, ti sarà richiesto di riavviare. Fai clic su **Close**.
7. Torna a **System** e fai clic su **Reboot**.
8. Dopo l'upgrade, chiudi tutte le istanze del browser e pulisci la cache del tuo computer prima di accedere all'applicazione.


L'interfaccia utente potrebbe essere diversa a seconda della versione corrente del tuo NetScaler VPX.
{: note}

Se stai eseguendo l'upgrade da NetScaler versione 11 a 12, la funzione CallHome è abilitata per impostazione predefinita anche se l'hai specificatamente disabilitata prima e durante l'installazione. Per disabilitare questa funzione, puoi utilizzare la riga di comando o la IU di gestione Citrix:

   * Riga di comando: `disable feature CallHome`
   * IU di gestione Citrix:

     1. Vai a **Configuration** > **System** > **Settings**.
     2. Nel pannello dei dettagli, fai clic sul link **Configure Advanced features** e deseleziona l'opzione **Callhome**.
     3. Fai clic su **OK**.
     {: note}
