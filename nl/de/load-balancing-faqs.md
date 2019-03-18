---
copyright:
  years: 1994, 2017

lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}

# Häufig gestellte Fragen zu Citrix NetScaler VPX
{: #faqs-for-citrix-netscaler-vpx}

Im Folgenden werden häufig gestellte Fragen (FAQs = Frequently Asked Questions) aufgeführt, die beim Einsatz von Citrix NetScaler VPX auftreten können.

## Was ist Citrix NetScaler VPX?
{:faq}

Citrix NetScaler ist ein Anwendungsbereitstellungscontroller, der Anwendungen in mehrfacher Hinsicht optimiert, und zwar durch die Verbesserung der Leistung, die Sicherstellung der Anwendungsverfügbarkeit und des Anwendungsschutzes sowie durch eine erhebliche Reduzierung der Betriebskosten. Wählen Sie die Citrix NetScaler-Edition aus, die Ihren Anwendungsanforderungen optimal entspricht, und stellen Sie diese Edition auf einem geeigneten dedizierten System bereit, um Ihre Leistungsanforderungen zu erfüllen. Weitere Informationen zu Citrix NetScaler finden Sie auf der [NetScaler-Seite ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.citrix.com/products/netscaler-application-delivery-controller/overview.html){:new_window} auf der Citrix-Website.

## Wozu wird der Lastausgleich benötigt?
{:faq}

Der Lastausgleich für den Datenverkehr hat sich zu einem zentralen Aspekt zahlreicher Kundenimplementierungen entwickelt, da er zur Verteilung der Anwendungsanforderungen und der Auslastung auf mehrere Server dient. Außerdem bietet diese Funktion eine Reihe von Vorteilen für die Gesamttopologie:

* Sicherheit. Auf Basis von IP-Protokollen und Portnummern wird eine logische Isolation der Anwendungsserver oder die Zurückweisung von Datenverkehrsanforderungen ermöglicht.
* Hochverfügbarkeit (HA = High Availability). Inhalte werden in einen Pool oder in eine Gruppe von Servern repliziert, sodass ihre Verfügbarkeit für Hosts sichergestellt ist.
* Skalierbarkeit. Bei steigendem Bedarf können zusätzliche Server zu Ihrer Konfiguration hinzugefügt werden, die dann von der Lastausgleichsfunktion bei der Workloadverteilung mit einbezogen werden können.
* Effizienz. Ist die Lastausgleichsfunktion konfiguriert, können Workloads dynamisch verteilt werden. Ressourcen wie beispielsweise CPUs können so effizienter genutzt werden.

## Wie viele Lastausgleichsoptionen stehen in {{site.data.keyword.BluSoftlayer_notm}} zur Verfügung?
{:faq}

Eine detaillierte Gegenüberstellung der IBM© Lastausgleichsangebote finden Sie in den Abschnitten zum [Kennenlernen der Lastausgleichsfunktion](/docs/infrastructure/loadbalancer-service?topic=loadbalancer-service-explore).

## Unterstützt NetScaler IPv6?
{:faq}

Ja. Im öffentlichen Netz von {{site.data.keyword.BluSoftlayer_notm}} werden sowohl IPv6 als auch IPv4 unterstützt.

## Führt NetScaler einen Lastausgleich für Datenverkehr im privaten Netz durch?
{:faq}

Ja, NetScaler stellt das einzige Lastausgleichsprodukt für {{site.data.keyword.BluSoftlayer_notm}} dar, das auch im privaten Netz eingesetzt werden kann.

## Kann NetScaler so konfiguriert werden, dass anstelle der Quellen-IP der NetScaler-Appliance die Quellen-IP-Adresse des Clients gemeldet wird?
{:faq}

Ja, der Parameter **Use Source IP (USIP)** kann in der erweiterten NetScaler-Managementschnittstelle auf **YES** eingestellt werden, um die Meldung der Quellen-IP des Clients anstelle der Quellen-IP von NetScaler zu ermöglichen.

Das Aktivieren des USIP-Adressmodus für die Appliance erhöht die Flexibilität der Appliance durch die Möglichkeit, bei der Kommunikation mit dem Server die Client-IP-Adresse zu verwenden, die im IP-Header verfügbar ist. Durch die Aktivierung dieses Modus öffnet die Appliance Serververbindungen über die Client-IP-Adresse und ermöglicht außerdem das Factoring der Client-IP-Adresse bei der Wiederverwendung von Verbindungen. So ermöglicht dieser Modus die eingeschränkte Wiederverwendung pro Client auf Basis der Client-IP-Adresse.

## Welche Ports werden zum Austausch der HA-bezogenen Informationen zwischen den Knoten einer HA-Konfiguration benutzt?
{:faq}

Der Port 3010 wird zur Synchronisation und Befehlsweitergabe benutzt. Der UDP-Port 3003 wird zum Austausch von Heartbeatpaketen verwendet.

## Welche NetScaler VPX-Version enthält die Funktion für den globalen Serverlastausgleich (GSLB = Global Server Load Balancing)?
{:faq}

Platinum.

## Kann ich NetScaler in HA-Konfigurationen nutzen?
{:faq}

Ja, NetScaler VPX-Appliances unterstützen HA-Konfigurationen (HA = High Availability; Hochverfügbarkeit).

NetScaler VPX-Server sind nur dann redundant, wenn sie im HA-Modus mit einem Partner konfiguriert wurden. Im Rahmen Ihrer Sicherungs- und Wiederherstellungsstrategie sollten Sie unbedingt eine HA-Umgebung bereitstellen, wenn Sie mit NetScaler VPX arbeiten.

Auch für andere Hardware- und Softwarekomponenten ist die Bereitstellung von Redundanz wichtig. Dies gilt beispielsweise für die Stromversorgung und für lokale Festplatten, die möglicherweise noch nicht redundant konfiguriert wurden. Ein Ausfall dieser Komponenten kann zu Datenverlusten führen.

## Umfasst das NetScaler-Angebot für {{site.data.keyword.BluSoftlayer_notm}} die SSL-VPN-Funktionalität?
{:faq}

Ja, diese Funktion wird unter dem Namen NetScaler Gateway™ angeboten und gehört zum Lieferumfang aller Editionen.  Weitere Informationen zu dieser Funktion erhalten Sie auf der [Citrix-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.citrix.com/products/netscaler-adc/){: new_window}.
