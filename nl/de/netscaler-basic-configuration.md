---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Grundlegende Lastausgleichskonfiguration
Beispiel: Ein Unternehmen betreibt eine grundlegende Social-Community-Website. Dort können sich Endbenutzer ohne Angabe sensibler Daten für ein Konto registrierten, um anschließend die Anmeldung durchzuführen und Bilder ihrer Haustiere zu posten. Es stehen drei Web-/Anwendungsserver sowie ein Datenbankserver als Sicherungseinheit zur Verfügung. Die Domäne und das DNS (Domain Name System) werden über {{site.data.keyword.BluSoftlayer_notm}} gehostet. Da es sich um eine kleine Umgebung handelt, befinden sich das NetScaler-System sowie die Web-/Anwendungsserver alle in demselben VLAN (Virtual Local Area Network). Dies vereinfacht die Situation, da keine weiteren Konfigurationsmaßnahmen für NetScaler erforderlich sind, um eine grundlegende Lastausgleichsrichtlinie einzurichten. In der folgenden Prozedur wird eine vereinfachte Darstellung des Datenverkehrsflusses in dieser Instanz erläutert:

1. Ein Benutzer gibt die URL in den Browser ein.
2. Der DNS-Datensatz der URL verweist auf eine der öffentlichen VIPs (Virtual IP Address) auf dem NetScaler-System.
3. Das NetScaler-System empfängt den Datenverkehr über diese VIP und dokumentiert das verwendete Datenverkehrsprotokoll (Datenverkehr über den HTTP-Port 80).
4. Das NetScaler-System übergibt diesen Datenverkehr auf Basis der definierten Lastausgleichsmethode (Umlauf-, Persistenz-IP-Methode usw.) an einen der Server im Serverpool.
5. Der Server akzeptiert den Datenverkehr und der Benutzer stellt eine Verbindung her und meldet sich an.

Hierzu muss das NetScaler-System zur Verarbeitung dieses Datenverkehrs konfiguriert werden. Da die VIP, die IP-Adresse des DNS-Servers sowie die SNIP (Subnet IP Address) bereits konfiguriert wurden, ist die Konfiguration einfach. 

In der grafischen NetScaler-Benutzerschnittstelle (GUI) müssen Sie in der Konfigurationsanzeige das Element für das **Datenverkehrsmanagement** auf der linken Seite erweitern. Erweitern Sie den Teilbereich für den **Lastausgleich**. Anschließend müssen für NetScaler die Zielserver angegeben werden, die in die Lastausgleichsrichtlinie aufgenommen werden sollen. Gehen Sie hierzu wie folgt vor:

1. Klicken Sie unter "Lastausgleich" auf **Server**.
2. Klicken Sie auf **Hinzufügen**.
3. Geben Sie den Servernamen des Servers (z. B. "Web1") ein.
4. Geben Sie die IP-Adresse des Servers ein.
5. Lassen Sie das Feld für die **Datenverkehrsdomäne** leer, da Sie in diesem Szenario lediglich die standardmäßige Datenverkehrsdomäne verwenden werden.
6. Geben Sie die gewünschten Kommentare für diesen Server ein.
7. Klicken Sie auf **Erstellen**.

Wiederholen Sie diese Prozedur für alle Server im Pool.  

**TIPP:** Um Server einfach identifizieren zu können, verwenden Sie für die Server eines Pools eine einheitliche Namenskonvention (z. B. "Web1", "Web2", "Web3" usw.).

Als Nächstes müssen Sie die Services erstellen. Sie erstellen einen Service für jeden Server, den Sie eingegeben haben. Die Verbindung zwischen dem NetScaler-System und den Servern im Pool wird über den Service konfiguriert. Jeder Service verfügt über einen Namen und gibt eine IP-Adresse, einen Port und den Datentyp an, der bereitgestellt wird.

1. Klicken Sie auf die Optionen für **Datenverkehrsmanagement > Lastausgleich > Services**.
2. Klicken Sie auf **Hinzufügen**.
3. Erstellen Sie einen Service für jeden Server, der zuvor erstellt wurde, und verwenden Sie dabei die gleichen Informationen.

Als Nächstes müssen Sie einen virtueller Server erstellen. Der virtuelle Server stellt eine virtuelle Verbindung zwischen der für die Server mit Lastausgleich verwendeten VIP und den Services dar, die zuvor erstellt wurden.

1. Klicken Sie auf die Optionen für **Datenverkehrsmanagement > Lastausgleich > Virtuelle Server**.
2. Klicken Sie auf **Hinzufügen**.
3. Ordnen Sie dem virtuellen Server einen Namen zu.
4. Geben Sie das Protokoll (HTTP) an, für das der Lastausgleich durchgeführt werden soll.
5. Übernehmen Sie den IP-Adresstyp als Standardwert (IP-Adresse). Im Feld für die IP-Adresse geben Sie die VIP ein, die Sie als Eingangspunkt für alle Benutzer verwenden wollen.
6. Geben Sie den Port an. Der Standardport ist der Port 80.
7. Klicken Sie auf **OK**.

Binden Sie nun die von Ihnen erstellten Services an den virtuellen Server.

1. Klicken Sie in der Anzeige "Virtuelle Server" auf den Link für **Keine Servicebindung für virtuelle Lastausgleichsserver**.
2. Binden Sie jeden der zuvor erstellten Services an den virtuellen Server.
3. Klicken Sie auf **Fertig**.
4. Klicken Sie auf die Schaltfläche **Aktualisieren**. Der Status und der geltende Status werden nun grün angezeigt.

Sie haben nun einen Lastausgleichspool und eine Richtlinie für Ihre Website erstellt.
