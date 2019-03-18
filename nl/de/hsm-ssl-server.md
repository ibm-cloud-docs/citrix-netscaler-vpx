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

# Virtuellen SSL-Server hinzufügen und konfigurieren
{: #add-and-configure-the-ssl-virtual-server}

Gehen Sie wie folgt vor, um Ihren virtuellen SSL-Server hinzuzufügen und zu konfigurieren:

1. Navigieren Sie zu **System > Einstellungen > Basisfunktionen konfigurieren**. Wählen Sie **SSL-Auslagerung** aus und klicken Sie dann auf **OK**.
2. Navigieren Sie in der grafischen NetScaler-Benutzerschnittstelle (GUI) zu **Datenverkehrsmanagement > Lastausgleich > Services > Hinzufügen** und geben Sie den Namen sowie die IP-Adresse und als Protokoll **HTTP** an. Klicken Sie auf **OK**, um den Vorgang abzuschließen.
3. Überprüfen Sie, ob der Service betriebsbereit ist:

	<img src="images/15-confirm-service.png" alt="Zeichnung" style="width: 700px;"/>

4. Wiederholen Sie Schritt zwei für jeden weiteren Server.
5. Navigieren Sie zu **Datenverkehrsmanagement > Lastausgleich > Virtuelle Server>** und klicken Sie dann auf **Hinzufügen**. Geben Sie den Namen an und wählen Sie als Protokoll **SSL** aus. Anschließend geben Sie die öffentliche IP-Adresse ein. Klicken Sie auf **OK**, um den Vorgang abzuschließen.
6. Wählen Sie **Keine Servicebindung für virtuelle Lastausgleichsserver** aus und klicken Sie auf **Auswählen**. Wählen Sie die Services aus, die Sie in den vorherigen Schritten erstellt haben, und klicken Sie auf 'Auswählen'. Anschließend klicken Sie auf **Binden/Weiter**.

	<img src="images/18-bind-service.png" alt="Zeichnung" style="width: 700px;"/>

7. Schließlich klicken Sie auf **Kein Serverzertifikat** und dann auf **Serverzertifikat auswählen**. Wählen Sie das zuvor installierte Zertifikat aus. Klicken Sie auf **Auswählen**, dann auf **Binden/Weiter** und anschließend auf **Fertig**, um den Vorgang abzuschließen.
