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

# Konfiguration der Datenverkehrsweiterleitung des Forward Proxy mithilfe der {{site.data.keyword.vpx_full}}-Appliance
{: #configuring-forward-proxy-traffic-redirection-using-the-citrix-netscaler-vpx-appliance}

Dieser Leitfaden stellt eine schrittweise Konfigurationsanleitung für die Einrichtung eines Forward Proxys mithilfe der {{site.data.keyword.vpx_full}}-Appliance bereit. Diese Konfiguration wurde mit einer {{site.data.keyword.vpx_full}}-Appliance mit Softwareversion 11.1 (Platinum Feature Edition) und einer Leistung von 10 MB/s getestet.

<img src="images/fp1.png" alt="Zeichnung" style="width: 600px;"/>

## Durchgeführte Schritte

In dieser schrittweise aufgebauten Anleitung erfahren Sie, wie der Service konfiguriert wird.

Task  | Beschreibung
------------- | -------------
[{{site.data.keyword.vpx_full}}-Appliance bestellen](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-citrix-netscaler-vpx-appliance) | Als Erstes wird eine {{site.data.keyword.vpx_full}}-Appliance bestellt.
[Privates Teilnetz anfordern](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-request-a-private-subnet) | Fordern Sie ein privates Teilnetz für Ihr Konto vom IBM© Support an.
[Funktionen für Cacheweiterleitung und Lastausgleich aktivieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-enable-cache-redirection-and-load-balancing-capabilities) | Ermitteln Sie die Ressourcen Ihrer Anwendung, z. B. Ursprungspools und Statusprüfungsverfahren.
[Virtuellen DNS-Server konfigurieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-the-dns-virtual-server) | DNS-Auflöser hinzufügen, DNS-Servicegruppe definieren und dann den virtuellen DNS-Server definieren.
[Cacheweiterleitung für HTTP- oder HTTPS-Datenverkehr konfigurieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-http-s-traffic) | Konfigurieren Sie die Cacheweiterleitung für Ihren virtuellen Forward Proxy-Server mit HTTP- oder HTTPS-Datenverkehr.
[Cacheweiterleitung für SSL-Datenverkehr konfigurieren (optional)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-cache-redirection-for-ssl-traffic-optional-) | Konfigurieren Sie die Cacheweiterleitung für Ihren virtuellen Forward Proxy-Server mit SSL-Datenverkehr anstelle von HTTP oder HTTPS.
[Quellen-NAT für abgehenden Datenverkehr konfigurieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configure-source-nat-for-outbound-traffic) | Verwenden Sie Ihre {{site.data.keyword.vpx_full}}-Appliance für die Netzadressumsetzung (Network Address Translation, NAT) im abgehenden Datenverkehr von Ihren Clientmaschinen.
[Proxy-Einstellungen im Internet-Browser der Clientmaschine aktualisieren (optional)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-update-the-proxy-settings-on-the-client-machine-s-internet-browser-optional-) | Aktualisieren Sie wahlweise die Proxy-Einstellungen mit dem Internet-Browser Ihrer Clientmaschine.
