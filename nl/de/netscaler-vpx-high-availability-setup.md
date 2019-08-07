---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.vpx_full}} für High Availability (HA) konfigurieren
{: #setting-up-citrix-netscaler-vpx-for-high-availability-ha-}

Lastausgleichsfunktionen werden zum Lastausgleich für den Datenverkehr auf mehrere Anwendungsserver benutzt, um so die Leistung und Stabilität einer skalierbaren Anwendung zu verbessern. Allerdings stellt eine einzige Lastausgleichsfunktion auch einen Single Point of Failure dar. Dies kann vermieden werden, indem Sie ein HA-Paar (HA = High Availability; Hochverfügbarkeit) für NetScaler VPX konfigurieren. Zur Konfiguration eines HA-Paares werden zwei NetScaler VPX-Server benötigt. Der sekundäre Server übernimmt dabei die Lastausgleichsfunktion, falls der primäre Server ausfällt. 

Die SNIP (SubNet IP) stellt die IP dar, die von den Servern mit Lastausgleich als die Quellen-IP der Anforderungen (Verbindungen) erkannt wird, die an die VIP (Virtual IP Address) von NetScaler VPX abgesetzt werden. Normalerweise wird in einer Konfiguration mit einem HA-Paar die SNIP nicht geändert. Während einer Funktionsübernahme (Failover) kann dieser Fall jedoch eintreten. Wenn sich die beiden NetScaler-Systeme in demselben Teilnetz befinden, dann kann sich die SNIP des sekundären NetScaler VPX-Systems in die SNIP ändern, die ursprünglich vom primären NetScaler VPX-System verwendet wurde. Dies hat jedoch keine Unklarheiten für die Server zur Folge, die die Anforderung verarbeiten.

Für eine HA-Konfiguration müssen sich beide NetScaler-Systeme in demselben VLAN und in demselben Teilnetz befinden.

Vor der Erstellung der HA-Konfiguration müssen Sie sicherstellen, dass die folgenden Aktionen bereits ausgeführt wurden:

1. Wenn das Paar als Aktiv/Aktiv konfiguriert wird, dann müssen alle VIP-Teilnetze, die zu den Instanzen hinzugefügt werden, den Typ "Routed to VLAN" aufweisen.
2. Wenn das Paar als Aktiv/Passiv konfiguriert wird, dann müssen alle VIP-Teilnetze, die zu den Instanzen hinzugefügt werden, entweder den Typ "Routed to VLAN" oder den Typ "Secondary routed to IP" aufweisen. Sie müssen an die öffentliche IP-Adresse des primären Knotens weitergeleitet werden.

Nach der Bestellung der beiden NetScaler VPX-Server in dem erforderlichen VLAN und nach der Bestellung der VIP- und SNIP-Teilnetze zur Erfüllung der Anforderungen für die Konfiguration Ihres HA-Paars können Sie wie folgt fortfahren:

1. Öffnen Sie zwei Browserfenster und melden Sie sich auf beiden NetScaler-Systemen bei der erweiterten Schnittstelle an. Rufen Sie auf dem sekundären NetScaler-System **System > Benutzerverwaltung > Benutzer** auf und geben Sie als Rootkennwort das gleiche Kennwort wie auf dem primären NetScaler-System an. Aktualisieren Sie anschließend die Kennwortdatei im Portal von {{site.data.keyword.BluSoftlayer_notm}} auf der Gerätedetailseite, sodass die Angabe mit dem Kennwort für die sekundäre Einheit übereinstimmt.

2. Klicken Sie auf dem VPX-System, das als sekundäres System fungieren soll, auf die Optionen für **System > Hochverfügbarkeit** und dann mit der rechten Maustaste auf die erste Zeile. Klicken Sie anschließend auf **Bearbeiten**. Wählen Sie in der Dropdown-Liste für die Konfiguration des Hochverfügbarkeitsstatus die Option zum **Erhalten des sekundären Status** aus und klicken Sie dann auf **OK**.

3. Wählen Sie **Hinzufügen** aus. Geben Sie die IP-Adresse des Systems für das andere VPX-System (auf der Registerkarte "Hochverfügbarkeit" des primären Systems) und dann unten in der Anzeige die Details für die Rootanmeldung ein. Wählen Sie das Kästchen **INC aktivieren** nicht aus. Klicken Sie auf **OK**. 
	
	Wird nun ein Fehler ausgegeben, in dem Sie darüber informiert werden, dass sich die IPs nicht in demselben Teilnetz befinden, dann befinden sich die beiden VPX-Server möglicherweise nicht in demselben VLAN. Andernfalls können Sie nun den primären Server öffnen und die Schaltfläche **Aktualisieren** auswählen, um zu überprüfen, ob beide Server im HA-Modus arbeiten. 

	Die neue NetScaler-Management-IP für die sekundäre Einheit gibt eine IP-Adresse an, die um den Wert "1" niedriger liegt als zuvor. Wenn kein Zugriff auf das sekundäre VPX-System möglich ist, dann entfernen Sie die Hochverfügbarkeit wie folgt über die Befehlszeile:

	`sh ha node`

	Entfernen Sie dann die Angabe für den HA-Knoten:
	
	`rm ha node 1`

4. Auf dem primären VPX-System ist nun ersichtlich, dass für das ferne VPX-System eine Synchronisation durchgeführt wird. Rufen Sie den sekundären Server auf und überprüfen Sie die Konfiguration unter **Netz > IPs**. Nun wird die VIP des primärer Servers angezeigt. Die anderen aufgelisteten IPs werden als passiv ausgewiesen.

6. Rufen Sie wieder **System > Hochverfügbarkeit** auf dem sekundären Server auf und klicken Sie dann auf **Bearbeiten**. Wählen Sie in der Dropdown-Liste **AKTIVIERT** aus und klicken Sie dann auf **OK**.

7. Erzwingen Sie zu Testzwecken eine Funktionsübernahme. Aktualisieren Sie die Anzeige und überprüfen Sie, ob die IP-Adressen des sekundären Servers nun aktiviert werden. Führen Sie eine weitere Funktionsübernahme durch und überprüfen Sie, ob die Adressen nun wieder inaktiviert werden. Setzen Sie ein Pingsignal an die IPs ab, um sicherzustellen, dass diese ordnungsgemäß arbeiten.

8. Der primäre Server sollte nun als primärer Server gekennzeichnet sein und auf dem sekundären Server sollte gemeldet werden, dass die Synchronisation erfolgreich abgeschlossen wurde.
