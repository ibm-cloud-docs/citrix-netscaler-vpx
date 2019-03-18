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

# IBM Hardware Security Module (HSM) initialisieren
{: #initialize-ibm-hardware-security-module-hsm-}

Bei den meisten Konfigurationen muss die HSM-Einheit initialisiert werden. Ohne Initialisierung können nur bestimmte `show`-Befehle ausgeführt werden.

Gehen Sie wie folgt vor, um Ihre Einheit zu initialisieren:

1.	Stellen Sie eine Verbindung zur IBM© Hardware Security Module-Einheit über SSH her. Verwenden Sie hierbei die im Steuerungsportal unter **Einheiten > Einheitenliste > HSM-Namen einblenden** aufgelisteten Berechtigungsnachweise.

	Sie können stattdessen auch die Authentifizierung über öffentlichen Schlüssel ausführen. Weitere Informationen finden Sie im [Administratorhandbuch für die Appliance (Seite 38) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}.

	**HINWEIS:** SSH-Zugriff ist in der Regel aktiviert und standardmäßig zulässig. Wenn Sie Probleme beim Herstellen der Verbindung mit SSH haben, überprüfen Sie das Routing und die Sicherheit Ihrer Infrastruktur.

2. Führen Sie den Befehl `hsm init` aus:

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

	Die verwendete Syntax lautet hierbei wie folgt: `hsm init -l <hsmlabel>`

Mit dem Parameter `-l` wird dem HSM eine ID zugeordnet. Hierbei kann es sich um einen beliebigen aussagekräftigen Text oder eine beliebige aussagekräftige Beschreibung handeln, der bzw. die sich auf das Unternehmen, den Administrator oder die zu erfüllende Rolle bezieht. Das HSM-Administratorkennwort wird das designierte Kennwort für den HSM-Sicherheitsbeauftragten (SO) und ist im Wesentlichen ein Profil, das für die Erstellung und Konfiguration von Verschlüsselungsobjekten und für Änderungen der HSM-Umgebung benötigt wird.

Schließlich ist die Klondomäne eine gemeinsam genutzte ID, die es ermöglicht, dass Objekte in einer Gruppe von HSMs gebildet werden. Sie wird normalerweise für die Sicherung und/oder die Hochverfügbarkeit verwendet.

Die in der HSM-Befehlszeilenschnittstelle unterstützten und verfügbaren Befehle finden Sie im [LunaSH-Befehlsreferenzhandbuch![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window}.
