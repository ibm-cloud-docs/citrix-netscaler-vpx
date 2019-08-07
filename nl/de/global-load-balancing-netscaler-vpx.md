---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Globaler Serverlastausgleich mit {{site.data.keyword.vpx_full}}
{: #global-load-balancing-with-citrix-netscaler-vpx}

Beim globalen Serverlastausgleich (GSLB = Global Server Load Balancing) handelt es sich um ein Verfahren, mit dem der Datenverkehr auf mehrere Server bzw. Instanzen verteilt werden kann, die sich normalerweise in unterschiedlichen geografischen Regionen befinden. Dieses Konzept basiert auf einer globalen Einheit (Engine/Server) für den Lastausgleich, die Datenverkehrsanforderungen von Clients empfängt und diese Anforderungen an eine bestimmte Region weiterleitet. Dabei wird die Zielregion anhand von Kriterien und Algorithmen bestimmt, die vom Administrator ausgewählt und konfiguriert werden. Hierzu können im Netz von {{site.data.keyword.BluSoftlayer_notm}} zwei anerkannte Methoden verwendet werden:

* **CDN:** Das CDN (Content Delivery Network; Netz zur Bereitstellung von Inhalten) dient zur Bereitstellung von Inhalten und Rich-Media-Komponenten wie beispielsweise Bildern und Videos. Das CDN verteilt diese Inhalte geografisch über die verteilt liegenden Knoten, und zwar auf eine Weise, die möglichst geringe Latenzzeiten und die größtmögliche Geschwindigkeit garantieren. Es wird normalerweise implementiert, wenn lediglich bestimmte Inhaltselemente und nicht vollständige Websites oder Anwendungen verteilt werden müssen. {{site.data.keyword.BluSoftlayer_notm}} bietet diesen Service. Weitere Informationen zu diesem Thema erhalten Sie [hier](/docs/infrastructure/CDN?topic=CDN-getting-started). 
* **NetScaler VPX:** VPX verwendet eine ähnliche Objekthierarchie, wie sie auch beim regulären lokalen Lastausgleich eingesetzt wird, um den Datenverkehr auf verschiedene Regionen zu verteilen. Mithilfe DNS-basierter globaler Suchoperationen wählt NetScaler den Datensatz aus, der dem ausgewählten Standort bzw. der ausgewählten Site zugeordnet ist. Die Auswahl basiert auf den vom Administrator vorkonfigurierten Kriterien. Die eingehenden Abschnitte werden auf Basis dieser Option bzw. dieses Angebots erweitert.

Beachten Sie hierbei, dass andere Verfahren für die Verteilung von Inhalten zur Verfügung stehen. Hierzu zählt beispielsweise die HTTP-Weiterleitung, die ebenfalls mit {{site.data.keyword.vpx_full}} implementiert werden kann. 

## Informationen zu GSLB unter VPX

NetScaler VPX kann mit GSLB (Global Server Load Balancing) genutzt werden. Dazu muss lediglich die entsprechende Funktion in der CLI (Command Line Interface) oder GUI (Graphical User Interface) aktiviert werden. 

GSLB verwendet Komponenten und Objekte, die große Ähnlichkeit mit den Komponenten und Objekten aufweisen, die auch in Bereitstellungen mit lokalem Lastausgleich eingesetzt werden, wo Entitäten anhand eines hierarchischen Modells definiert werden.

GSLB kann zu verschiedenen Zwecken implementiert werden. Beispiele:

* **Lastverteilung/Lastausgleich:** Zur effizienten und intelligenten Verteilung von Ressourcen zwischen mehreren Standorten.
* **Wiederherstellung nach einem Stör-/Katastrophenfall:** Wird verwendet, wenn der Haupt- oder Primärstandort ausfällt oder den Service nicht mehr bereitstellen kann. In diesem Szenario kann ein alternativer Ausweichstandort die Verarbeitung übernehmen.
* **Leistung/Shaping:** Durch dieses Verfahren wird es möglich, Inhalte näher bei den Endsystemen oder in einer Weise zu positionieren, durch die die Leistung des betreffenden Service verbessert werden kann.

Die Hauptkomponenten oder -entitäten im GSLB-Prozess und bei der GSLB-Bereitstellung sind:

* **Virtuelle Server:** Bei einer VIP (Virtual IP Address) handelt es sich um eine IP-Adresse, an die Clients Anforderungen senden können. NetScaler beendet die Clientverbindung mit der VIP und stellt dann eine Verbindung zu einem Server her, der im (lokalen) Lastausgleichsservice konfiguriert ist. 
* **DNS (Domain Name System) und Namensserver:** Die Namensauflösung unter GSLB arbeitet nach einem ähnlichen Verfahren wie ein normales DNS. Der Unterschied betrifft die Logik und die Kriterien, die zur Bestimmung der aufgelösten Adressen verwendet werden. GSLB verwendet eine vorkonfigurierte Lastausgleichsmethode, um diese Auflösung durchzuführen. NetScaler kann auf unterschiedliche Weise zur Interaktion mit einem DNS konfiguriert werden:
	* ADNS (Authoritative DNS; autoritatives DNS). NetScaler-Systeme, die im ADNS-Modus arbeiten, haben für bestimmte Domänen und alle darin befindlichen Datensätze autoritativen Status.
	* DNS-Subdelegation. Die Subdelegation tritt auf, wenn ein (für die Domäne autoritativer) DNS-Server die Verantwortlichkeit für eine Unterdomäne an ein NetScaler-System delegiert.
	* DNS-Proxy. Sind NetScaler-Systeme in diesem Modus konfiguriert, dann leiten sie DNS-Anforderungen an einen anderen (externen) Server weiter, der die Namensauflösung durchführt.
* **Methode:** Bei der Methode handelt es sich um einen Algorithmus, der vom virtuellen GSLB-Server zur Auswahl des am besten geeigneten GSLB-Service der Topologie verwendet wird. Der Algorithmus bewertet die Leistungsaspekte, die den eigentlichen Auswahlkriterien zugeordnet sind. Folgende Methoden stehen zur Verfügung:
  * Umlaufmethode: Verteilt eingehende Anforderungen unabhängig von deren Auslastung auf die verfügbaren GSLB-Sites und -Services.
  * RTT-Methode (RTT = Round Trip Time; Umlaufzeit): Diese Methode basiert auf einer Kennzahl für die zwischen dem lokalen DNS-Server und den (GSLB-)Sites erforderlichen Zeitaufwänden und der in diesem Bereich auftretenden Verzögerungen. NetScaler verwendet unterschiedliche Mechanismen (z. B. ICMP-Echoanforderung/-antwort (PING), UDP und TCP), um die RTT-Metriken zu erfassen.
  * Methode mit statischer Nähe: Bei dieser Methode wird eine Datenbank mit IP-Adressen verwendet, um die Nähe zwischen dem lokalen DNS-Server des Clients und den Sites (Standorten) zu erfassen. Anschließend werden die so ermittelten Kriterien verwendet, um eine Auswahl zu treffen.
  * Methode mit geringster Verbindungsanzahl: Bei dieser Methode wird die geringste Anzahl aktiver Verbindungen pro Site/Service gemessen und als Auswahlkriterium verwendet.
  * Methode mit kürzester Antwortzeit: Bei dieser Methode wird die Site mit der geringsten Anzahl aktiver Verbindungen und der niedrigsten durchschnittlichen Antwortzeit ausgewählt.
  * Methode mit geringster Bandbreite: Bei dieser Methode wird die Site ausgewählt, die momentan das geringste Datenverkehrsaufkommen (Mbps) verarbeitet.
  * Methode mit geringster Paketanzahl: Bei dieser Methode wird der Service ausgewählt, der innerhalb der letzten 14 Sekunden die geringste Anzahl an Paketen empfangen hat.
  * Methode mit Hashing für Quellen-IP-Adresse: Bei dieser Methode wird der Service auf Basis des Hashwerts der IPv4- und der IPv6-Adresse des Clients ausgewählt.
  * Angepasste Auslastung: Bei dieser Methode wird der Service ausgewählt, der momentan keine aktiven Transaktionen verarbeitet. Wenn alle Services in der Lastausgleichskonfiguration aktive Transaktionen verarbeiten, dann wählt die Appliance den Service mit der geringsten Auslastung (CPU-Auslastung, Speicherauslastung und Antwortzeit) aus.

* **MEP (Metric Exchange Protocol):** Ein proprietäres Protokoll, das zum Austausch von Metriken (Auslastung und Netz) sowie Persistenzdaten zwischen Sites verwendet wird. MEP dient zur Statusprüfung zwischen unterschiedlichen Sites und NetScaler-Systemen im GSLB-Netz bzw. innerhalb der GSLB-Topologie. Bei Verwendung der vom Administrator festgelegten Kriterien bietet MEP eine Möglichkeit, mit deren Hilfe Sites kommunizieren und den Datenverkehr auf Basis der Auswahlparameter verarbeiten können, die zuvor konfiguriert wurden. MEP verwendet die TCP-Ports mit den Nummern 3009 und 3011. Wird MEP inaktiviert, dann ist die Methodenauswahl auf die hier aufgeführten Optionen beschränkt, die mit einem Stern (*) markiert sind. Bei Auswahl nicht markierter Methoden verwendet das System die Umlaufmethode.
* **Überwachung:** Die NetScaler-Engine bewertet in regelmäßigen Zeitabständen den Status der fernen GSLB-Services. Dazu verwendet das System entweder MEP oder explizite Überwachungsfunktionen, die über eine Bindung zu den betreffenden Services verfügen. Überwachungsfunktionen werden dabei in derselben Weise verwendet, wie dies bei einem regulären Lastausgleichsservice der Fall ist. Bei GSLB ist das Hinzufügen von Überwachungsfunktionen zu den lokalen Services nicht erforderlich, da dieser Bereich normalerweise von MEP gesteuert wird. 
* **Persistenz:** Eine optionale Funktion, die eine Sitevorgabe für eine bestimmte Domäne erstellt. In diesem speziellen Anwendungsfall wird für den Datenverkehr kein Lastausgleich durchgeführt. Er wird stattdessen über dasselbe Rechenzentrum verarbeitet. Diese Vorgehensweise kann in bestimmten Anwendungen (z. B. E-Commerce-Anwendungen) hilfreich sein, in denen die Transaktionsdaten für die Sites/Server eindeutig sind.
* **GSLB-Site:** Sites können als Rechenzentren oder Standorte definiert werden, für die ein NetScaler-System konfiguriert wurde und verfügbar ist. Jede GSLB-Site wird von einem NetScaler-System verwaltet, das als "lokal" in Bezug auf diese Site eingestuft wird, während alle anderen fernen Systeme/Sites als "fern" eingestuft und behandelt werden.
* **GSLB-Service:** Hierbei handelt es sich um ein Objekt, das einen (regulären) virtuellen Server bzw. eine (reguläre) virtuelle IP-Adresse (VIP) darstellt (und an diesen virtuellen Server bzw. diese virtuelle IP-Adresse gebunden ist). Der Service kann lokal (an derselben Site) oder fern bereitgestellt werden.
* **Virtueller GSLB-Server:** Ein virtueller GSLB-Server ist mindestens einem GSLB-Service zugeordnet, der normalerweise auf unterschiedlichen (GSLB-)Sites zum Einsatz kommt. Der dort eingehende Datenverkehr wird über die Lastausgleichsfunktion auf die verschiedenen zugeordneten Sites verteilt. Die Siteauswahl wird auf Basis der verwendeten Methode und des jeweiligen Anwendungsfalls durchgeführt.
* **GSLB-Domäne:** Gibt die Domäne oder Zone an, für die der virtuelle GSLB-Server verantwortlich ist. 
* **ADNS-Service:** Dieser Service wird durch eine Kombination aus IP-Adresse und Port dargestellt und gibt an, wohin die DNS-Anforderungen an eine Domäne, für die NetScaler autoritativen Status hat, gesendet werden. NetScaler leitet die Daten an den virtuellen GSLB-Server weiter, der dieser Domäne zugeordnet ist, um eine Antwort zu erhalten.
