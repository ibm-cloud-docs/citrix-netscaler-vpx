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

# Cacheweiterleitung für HTTP- oder HTTPS-Datenverkehr konfigurieren
{: #configure-cache-redirection-for-ssl-traffic-optional-}

Gehen Sie wie folgt vor, um die Cacheweiterleitung für HTTP- oder HTTPS-Datenverkehr zu konfigurieren:

1. Rufen Sie die Optionen für **Datenverkehrsmanagement > Cacheweiterleitung > Virtuelle Server** auf und klicken Sie dann auf **Hinzufügen**.
2. Geben Sie den Namen des virtuellen Servers für den Forward Proxy an. Wählen Sie das Protokoll **HTTP** und den Cachetyp **Forward** in den entsprechenden Dropdown-Listen aus. Ordnen Sie dann diesem virtuellen Server eine IP-Adresse aus Ihrem privaten Teilnetz zu.

	<img src="images/fp12.png" alt="Zeichnung" style="width: 300px;"/>

	Klicken Sie auf **OK**, um fortzufahren.

3. Überprüfen Sie die Übersichtsseite und klicken Sie auf **OK**.  
4. Klicken Sie auf **Datenverkehrseinstellungen**, um weitere Konfigurationseinstellungen anzuzeigen.
5. Wählen Sie in den Datenverkehrseinstellungen eine der folgenden drei Weiterleitungsoptionen aus. Die Auswahl ist von Ihren Anforderungen abhängig.
	* **Cache** - Bei dieser Auswahl werden alle abgehenden Anforderungen an Ihren lokalen Cache-Server-Pool weitergeleitet.
	* **Richtlinie** - Bei dieser Auswahl wird die Cacheweiterleitungsrichtlinie überprüft, um festzustellen, ob die Anforderung an den Cache-Server-Pool oder an die Zielserver (Ursprung) weitergeleitet werden soll.
	* **Ursprung** – Bei dieser Auswahl werden alle abgehenden Anforderungen an die jeweiligen Zielserver (Ursprung) weitergeleitet.

6. Wählen Sie in der Dropdown-Liste mit den **Namen des virtuellen DNS-Servers** den zuvor konfigurierten virtuellen DNS-Server aus und geben Sie **Ursprung** für die Option **Weiterleiten** an.

	<img src="images/fp13.png" alt="Zeichnung" style="width: 300px;"/>

	**HINWEIS:** Die Einstellung für den **virtuellen Zielserver** wird verwendet, wenn abgehender Datenverkehr an den lokalen Cache-Server-Pool weitergeleitet werden soll. Lassen Sie die Einstellung leer, wenn Sie den gesamten abgehenden Datenverkehr an Ursprungsserver weiterleiten wollen.

7. Klicken Sie auf **OK** und anschließend auf **Fertig**.
