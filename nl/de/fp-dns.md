---



copyright:
  years: 2017
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Virtuellen DNS-Server konfigurieren
{: #configure-the-dns-virtual-server}

Gehen Sie wie folgt vor, um einen virtuellen DNS-Server zu konfigurieren:

1. Wählen Sie 'Datenverkehrsmanagement > Lastausgleich > Server' aus. 
2. Klicken Sie auf 'Hinzufügen', um die beiden IBM© Softlayer-DNS-Auflöser (10.0.80.11 und 10.0.80.12) hinzuzufügen. 

	<img src="images/fp5.png" alt="Zeichnung" style="width: 200px;"/> <img src="images/fp5b.png" alt="Zeichnung" style="width: 200px;"/>

3. Erstellen und definieren Sie anschließend Ihre DNS-Servicegruppe, indem Sie auf 'Datenverkehrsmanagement > Lastausgleich > Servicegruppen' klicken und 'Hinzufügen' auswählen. 

	<img src="images/fp6.png" alt="Zeichnung" style="width: 400px;"/> 

4. Wählen Sie das DNS-Protokoll aus und klicken Sie dann auf OK.

	<img src="images/fp7.png" alt="Zeichnung" style="width: 300px;"/> 
	
5. Fügen Sie in der nächsten Anzeige die neuen DNS-Auflöser dieser DNS-Servicegruppe als Member-Server hinzu. Klicken Sie hierfür zunächst auf das leere Feld unter **Servicegruppenmitglieder**. 

6. Geben Sie in der Anzeige 'Servicegruppenmitglied erstellen' DNS-Port 53 an und klicken Sie dann auf 'Erstellen'. 

	<img src="images/fp8.png" alt="Zeichnung" style="width: 200px;"/> 
	
7. Klicken Sie auf 'Schließen' und dann auf 'Fertig'. 

	Wenn die beiden IBM Softlayer-DNS-Auflöser von Ihrer Citrix NetScaler VPX-Appliance aus erreichbar sind, wird die Servicegruppe grün angezeigt. 

8. Klicken Sie jetzt auf 'Datenverkehrsmanagement > Lastausgleich > Virtuelle Server' und dann auf 'Hinzufügen', um Ihren virtuellen DNS-Server zu definieren.
9. Ordnen Sie unter 'Basiseinstellungen' Ihrem virtuellen Server einen Namen zu, wählen Sie das Protokoll DNS und Port 53 aus und ordnen Sie dann eine IP-Adresse aus Ihrem privaten Teilnetz zu. 

	<img src="images/fp9.png" alt="Zeichnung" style="width: 300px;"/> 
	
10. Klicken Sie auf der folgenden Seite auf das leere Feld **Keine Servicegruppenbindung für virtuelle Lastausgleichsserver**.
11. Wählen Sie Ihre zuvor definierte DNS-Servicegruppe in der Dropdown-Liste aus und klicken Sie auf 'Binden'.  

	<img src="images/fp10.png" alt="Zeichnung" style="width: 300px;"/> 
	
12. Klicken Sie auf 'Weiter' und anschließend auf 'Fertig'. 

Der Status des virtuellen DNS-Servers sollte jetzt grün angezeigt werden. 

<img src="images/fp11.png" alt="Zeichnung" style="width: 500px;"/> 
