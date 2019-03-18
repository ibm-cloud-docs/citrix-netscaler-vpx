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

# Cacheweiterleitung für SSL-Datenverkehr konfigurieren (optional)
{: #configure-cache-redirection-for-ssl-traffic-optional-}

Anstelle der Cacheweiterleitung für den virtuellen Server mit einem HTTP- oder HTTPS-Protokoll (siehe den vorherigen Schritt) können Sie dafür auch die Abwicklung des SSL-Datenverkehrs definieren. 

Gehen Sie hierfür wie folgt vor:

1. Rufen Sie die Optionen für **Datenverkehrsmanagement > Cacheweiterleitung > Virtuelle Server** auf und klicken Sie dann auf **Hinzufügen**. Geben Sie den Namen für Ihren virtuellen Server des Forward Proxys an und wählen Sie das SSL-Protokoll sowie den Cachetyp **FORWARD** aus. Ordnen Sie ihm eine IP-Adresse aus Ihrem privaten Teilnetz mit dem erforderlichen Port zu. 

	<img src="images/fp14.png" alt="Zeichnung" style="width: 300px;"/>

	Klicken Sie auf **OK**. 
	
2. Überprüfen Sie die Übersichtsseite und klicken Sie auf **OK**, um fortzufahren.
3. Geben Sie die Konfigurationen für die Weiterleitung, den virtuellen DNS-Server und den virtuellen Zielserver an. 
4. Klicken Sie auf **Zertifikat** unter dem Bereich **Erweiterte Einstellungen**, um die Konfiguration für SSL-Zertifikate anzuzeigen. 
5. Klicken Sie auf das leere Feld **Kein Serverzertifikat**.
6. Wählen Sie Ihren SSL-Server in der Dropdown-Auswahlliste für Serverzertifikate aus.
7. Geben Sie die Konfigurationsdaten für das Zertifikat nach Bedarf ein.

	<img src="images/fp15.png" alt="Zeichnung" style="width: 400px;"/>

	Klicken Sie auf **Installieren**.
	
8. Wählen Sie **Binden** aus.

	<img src="images/fp16.png" alt="Zeichnung" style="width: 300px;"/>
