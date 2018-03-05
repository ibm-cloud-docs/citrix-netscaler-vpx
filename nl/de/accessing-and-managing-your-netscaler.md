---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX - Zugriff und Verwaltung

Citrix NetScaler-Geräte stellen leistungsfähige Tools mit einer Palette von Funktionen dar, die Sie bei der Erweiterung und Optimierung Ihrer Lösung für {{site.data.keyword.BluSoftlayer_notm}} auf unterschiedlichste Weise unterstützen. Die Informationen Ihres Geräts erhalten Sie im Kundenportal. Dort können Sie auch die erforderlichen Geräteverbindungen herstellen und seine Funktionen konfigurieren.  

## NetScaler-Details im Kundenportal suchen

Citrix NetScaler-Geräte werden wie alle anderen Server der Plattform von {{site.data.keyword.BluSoftlayer_notm}} auch in der Einheitenliste aufgeführt.

Gehen Sie wie folgt vor, um die Einheitenliste zu suchen:

1. Öffnen Sie im Browser das [Kundenportal ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} und melden Sie sich bei Ihrem Konto an.
2. Wählen Sie in der Navigation des Kundenportals die Optionen für **Geräte > Geräteliste** aus.

Daraufhin werden Ihre Geräte nach Gerätename sortiert aufgelistet. Citrix NetScaler VPX-Geräte sind am Gerätetyp "NetScaler" zu erkennen. 

Klicken Sie auf der linken Seite der Zeile für Ihr NetScaler-System auf den Pfeil, um die Zeile zu erweitern und den Benutzernamen sowie ein maskiertes Kennwort für den NetScaler-Managementzugriff anzuzeigen. 

Die Geräteliste enthält außerdem die folgenden Detailangaben: 

* Standort (Rechenzentrum, in dem sich das NetScaler-System befindet)
* Private IP-Adresse (wird zur Herstellung der NetScaler-Verbindung für den Zugriff auf die Managementfunktionen benutzt)
* Startdatum (Zeitpunkt, zu dem das System bestellt und bereitgestellt wurde)

**HINWEIS:** Während die private IP-Adresse des NetScaler-Systems im Portal aufgelistet wird, ist die öffentliche IP-Adresse des NetScaler-Systems dort nicht aufgeführt. Dies ist darauf zurückzuführen, dass das Management des NetScaler-Systems mithilfe der privaten IP-Adresse durchgeführt wird, während die öffentlichen IP-Adressen von NetScaler-Geräten als VIPs oder virtuelle IPs des Geräts verwendet werden, die für die Lastausgleichsservices benötigt werden.

## Anzeige für Gerätedetails 

Wenn Sie auf den Namen des NetScaler-Systems klicken, dann wird die Seite mit den **Gerätedetails** dieses Systems aufgerufen. Auf dieser Seite finden Sie das VLAN (Virtual Local Area Network), in dem das NetScaler-System bereitgestellt wurde, und außerdem die öffentlichen IP-Adressen des NetScaler-Systems. Diese IP-Adressen dürfen nicht zu Managementzwecken verwendet werden, da sie die standardmäßigen öffentlichen VIPs (VIP = Virtual IP Address; virtuelle IP-Adresse) des NetScaler-Systems darstellen. Diese Adressen werden Sie später verwenden, um eine Zuordnung zu einem Service für den Lastausgleich herzustellen.

## NetScaler-System verwalten

{{site.data.keyword.BluSoftlayer_notm}} ermöglicht Ihnen den vollständigen Rootzugriff auf Ihr NetScaler-Gerät. Zur Anmeldung bei der Managementbenutzerschnittstelle des NetScaler-Systems müssen Sie mit dem privaten Netz für {{site.data.keyword.BluSoftlayer_notm}} verbunden sein. (Dazu müssen Sie entweder über ein Management-VPN für {{site.data.keyword.BluSoftlayer_notm}} verfügen oder die Managementfunktionen über eine ferne Sitzung auf einem Server in der Umgebung für {{site.data.keyword.BluSoftlayer_notm}} ausführen.) 

Um über das Kundenportal eine Verbindung zur Managementbenutzerschnittstelle des NetScaler-Systems herzustellen, müssen Sie auf die Dropdown-Liste **Aktionen** in der rechten oberen Ecke der Anzeige für die **Gerätedetails** klicken und dann die Option zum **Verwalten des Geräts** auswählen, um eine neue Registerkarte oder ein neues Popup-Fenster im Browser aufzurufen. Dadurch werden Sie zur NetScaler-NSIP (private IP-Adresse, die zuvor angezeigt wurde) weitergeleitet. Auf der nun angezeigten Seite werden Sie zur Eingabe des Rootbenutzernamens und des Kennworts Ihres Geräts aufgefordert. Nach Eingabe dieser Informationen wird die Managementbenutzerschnittstelle des NetScaler-Systems aufgerufen. 

Alternativ hierzu können Sie die private IP des NetScaler-Geräts auch kopieren und in einen Web-Browser einfügen.

### NetScaler-SSH-Zugriff

Es ist ebenfalls möglich, über den bevorzugten SSH-Client eine direkte Verbindung zu Ihrem NetScaler-Gerät herzustellen. Verwenden Sie die private IP und die entsprechenden Anmeldeinformation für das NetScaler-Gerät, die auf der Seite für die Geräteliste aufgeführt sind, und vergewissern Sie sich, dass eine Verbindung zum VPN (Virtual Private Network) für {{site.data.keyword.BluSoftlayer_notm}} besteht. 
