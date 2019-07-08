---
copyright:
  years: 1994, 2017
  
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung zur Citrix NetScaler VPX-Software-Appliance
{: #getting-started-with-citrix-netscaler-vpx-software-appliance}

Die Bereitstellung von Citrix NetScaler VPX in Ihrer Lösung für {{site.data.keyword.BluSoftlayer_notm}} beschleunigt die Webanwendungsbereitstellung, ermöglicht entscheidende Leistungsverbesserungen und gewährleistet, dass Ihre Cloudanwendungen und -services stets optimiert, verfügbar und sicher sind. Bei hohen Workloadanforderungen, wie sie beispielsweise im Gaming- und Big-Data-Bereich sowie bei Analyseanwendungen oder in privaten Clouds auftreten, kann Citrix NetScaler VPX Sie dabei unterstützen, Ihre Lösung stets zeitgerecht, am richtigen Standort und in optimaler Konfiguration für Ihre Benutzer bereitzustellen.

## Vorbereitungen
Für den Einstieg in Citrix NetScaler VPX benötigen Sie die folgenden Informationen:

* Anmeldeinformationen für das IBM© Cloud-Kundenportal
* Bereitstellungsposition für die Lastausgleichsfunktion
* Für die jeweiligen Anforderungen am besten geeigneter NetScaler-Typ (weitere Informationen finden Sie in [Lastausgleichsfunktionen erkunden](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore)
* Anzahl der benötigten öffentlichen IP-Adressen
* VLAN für die Zuweisung der Lastausgleichsfunktion

## Citrix NetScaler VPX bestellen

Zum Bestellen einer Citrix NetScaler VPX-Software-Appliance navigieren Sie auf die Bestellseite des Kundenportals:

1. Öffnen Sie im Browser das [Kundenportal ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} und melden Sie sich bei Ihrem Konto an.
2. Wählen Sie in der Navigation des Kundenportals die Optionen für **Geräte > Geräteliste** aus und klicken Sie dann auf den Link für die **Gerätebestellung**. 
3. Blättern Sie auf der Seite zur **Bestellung von SoftLayer-Produkten und -Services** bis zum Abschnitt für das Netz nach unten und klicken Sie dann auf den Link für **Bestellen** unter Citrix NetScaler VPX.
4. Wählen Sie im Dropdown-Menü einen Standort aus, an dem die Citrix NetScaler VPX-Software-Appliance bereitgestellt werden soll.  
5. Wählen Sie den NetScaler-Typ aus, der am besten zu Ihrer Softwareedition, Softwareversion und zu Ihren Durchsatzanforderungen passt. 
6. Wählen Sie die Anzahl der benötigten öffentlichen IP-Adressen aus.  
	Hierbei handelt es sich um statische öffentliche IP-Adressen, die als virtuelle IP-Adressen (VIPs) auf dem NetScaler VPX-System bereitgestellt werden.
7. Klicken Sie auf **Weiter**.
8. Geben Sie die für ARIN (American Registry for Internet Numbers) erforderlichen Informationen (oder die Informationen der entsprechenden Organisation in ihrer Bereitstellungsregion) für die angeforderten IP-Adressen an.
9. Geben Sie die Kontaktinformationen ein. 
10. Wählen Sie das gewünschte VLAN (Virtual Local Area Network) aus. 
	Zur Minimierung der Latenzzeiten und zur Sicherstellung einer optimierten Auslastung der Netzressourcen müssen Sie Citrix NetScaler VPX demselben VLAN zuweisen, dem auch die Server zugewiesen sind, auf denen der Datenverkehr verteilt wird. 
11. Überprüfen Sie die Bestellung, akzeptieren Sie die Vertragsbedingungen und klicken Sie dann auf **Bestellung aufgeben**. Die Citrix NetScaler VPX-Software-Appliance wird nun mit den von Ihnen ausgewählten Einstellungen bereitgestellt. 

## Weitere Schritte

Sie können weitere Informationen zu den [Features](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-about-citrix-netscaler-vpx) von Citrix NetScaler VPX aufrufen, sich mit der speziellen NetScaler-[Terminologie](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-citrix-netscaler-vpx-terminology) vertraut machen oder mit der [Konfiguration](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-basic-load-balancing-configuration) einer NetScaler-Instanz beginnen.
