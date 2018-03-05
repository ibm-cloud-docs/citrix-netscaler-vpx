---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-6"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Standardbereitstellung

Wenn Sie das NetScaler-System in der Anzeige für **Geräte > Geräteliste** im [Kundenportal ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/) überprüfen, dann werden Sie feststellen, dass dieses System anders dargestellt wird, wie dies bei anderen Servern der Fall ist. Dieses Gerät verfügt zwar über eine private IP-Adresse, jedoch nicht über eine öffentliche IP-Adresse.

Die Standardbereitstellung eines NetScaler-Systems in {{site.data.keyword.BluSoftlayer_notm}} ist auf größtmöglichste Sicherheit ausgelegt. Dazu wird zu Managementzwecken als NetScaler-IP (NSIP) automatisch eine private IP-Adresse zugewiesen. Wenn Sie auf den Pfeil links neben dem NetScaler-System klicken, dann wird die Zeile erweitert, um den Standardbenutzernamen (Root) und das maskierte Rootbenutzerkennwort anzuzeigen. 

{{site.data.keyword.BluSoftlayer_notm}} steuert eine Vielzahl der Entscheidungen, die während der Bereitstellung getroffen werden müssen. Hierzu gehört beispielsweise die Angabe, welche IP-Adresse für welchen Zweck verwendet werden soll. Des Weiteren muss angegeben werden, welche VLANs (Virtual Local Area Networks) zur Bereitstellung verwendet werden sollen. Außerdem wird ein Großteil der erforderlichen Back-End-Konfigurationsmaßnahmen mithilfe von Scripts und einer API (Anwendungsprogrammierschnittstelle) automatisiert. Diese Maßnahmen umfassen die Zuweisung von Schnittstellen zu unterschiedlichen öffentlichen und privaten VLANs sowie die Zuweisung der korrekten IP-Adressen (einschließlich NSIP, VIPs und SNIPs) zu den Schnittstellen.

## Welche Komponenten müssen konfiguriert werden?

Standardmäßig stellt die NSIP die private IP-Adresse dar, die während der Bereitstellung zugewiesen wird. Hierbei handelt es sich um die IP-Adresse, die zur Herstellung der Verbindung zum NetScaler-System zu Managementzwecken verwendet wird. Die SNIPs (IP-Teilnetzadressen) werden standardmäßig über dieselben primären IP-Teilnetze zugewiesen, die sich in den VLANs befinden, die sie während des Bestellablaufs auswählen. 

Wenn Sie dieselben VLANs auswählen, in denen sich auch die vorgesehenen Server mit Lastausgleich befinden, dann sind keine zusätzlichen Konfigurationsmaßnahmen für diese SNIPs erforderlich. Standardmäßig sind im DNS (Domain Name System) die Namensserver für {{site.data.keyword.BluSoftlayer_notm}} angegeben. In einer Basisimplementierung, in der {{site.data.keyword.BluSoftlayer_notm}} die DNS-Datensätze Ihrer Server hostet, sind dann keine weiterführenden Konfigurationsmaßnahmen erforderlich.
