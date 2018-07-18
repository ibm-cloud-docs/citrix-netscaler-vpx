---
copyright:
  years: 1994, 2018

lastupdated: "2018-06-28"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Upgrade für Citrix NetScaler VPX durchführen

**HINWEIS:** Sie müssen mit dem VPN (Virtual Private Network) verbunden sein, um diese Prozedur ausführen zu können.

1. Melden Sie sich bei der NetScaler-Management-IP an.
2. Klicken Sie auf den **Systemupgrade**.
4. Wählen Sie **Lokal** in der Dropdown-Liste **Datei auswählen** aus.  
4. Laden Sie die korrekte Upgradedatei von der folgenden Speicherposition herunter:

	[Verfügbare NetScaler-Versionen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}
	
	**Hinweis:** Für den Zugriff auf diesen Link muss eine Verbindung zum VPN der IBM Cloud-Infrastruktur bestehen.

5. Suchen Sie in der Anzeige für das Hochladen von Software nach der Speicherposition der Upgradedatei und klicken Sie dann auf **Upgrade**. Die Firmware wird hochgeladen.
6. Im daraufhin angezeigten Systemupgradefenster werden Sie aufgefordert, einen Neustart durchzuführen. Klicken Sie auf **Schließen**.
7. Kehren Sie zu **System** zurück und klicken Sie auf **Neu starten**.
8. Schließen Sie nach dem Upgrade alle Browserinstanzen und leeren Sie den Cache des Computers, bevor Sie auf die Appliance zugreifen.

**Hinweis:** Abhängig von der aktuellen NetScaler VPX-Version kann die Benutzerschnittstelle variieren.



