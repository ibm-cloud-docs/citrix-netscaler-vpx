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

# SSL-Auslagerung mit Citrix NetScaler VPX konfigurieren und optimieren
{: #configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx}

Diese schrittweise aufgebaute Anleitung führt Sie durch die Konfiguration und Optimierung der SSL-Auslagerung in Citrix NetScaler VPX. Dies geschieht mithilfe des Zertifikats und des Verschlüsselungsmaterials, das über den HSM-Link generiert wird.

**HINWEIS:** Voraussetzung für diese schrittweise Anleitung ist die Ausführung der Schritte in [IBM© Hardware Security Module (HSM) mit Citrix NetScaler VPX bereitstellen und konfigurieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx), um Ihr VPX/HSM-Paar bestellen und erstellen zu können.

## Informationen zur Bereitstellung
Diese Bereitstellung wurde mit den folgenden Komponentenspezifikationen erstellt und getestet:

| NetScaler VPX Version & Build	| HSM-Softwareversion | HSM-Firmwareversion | HSM-Clientversion |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |


## Logische Topologie
Das folgende Diagramm zeigt den Netzverkehrsdatenfluss für den Anwendungsfall 'SSL-Auslagerung'. Dieses Diagramm stellt eine visuelle und logische Perspektive des Trust-Links und der Konfiguration zwischen der Citrix VPX- und der HSM-Appliance bereit.

<img src="images/network-flows-logical-topology.jpg" alt="Zeichnung" style="width: 700px;"/>

Wenn Sie mit der SSL-Auslagerung nicht vertraut sind, lesen Sie diesen [Citrix-Artikel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html){:new_window}.

## Durchgeführte Schritte

In dieser schrittweise aufgebauten Anleitung erfahren Sie, wie SSL für eine Citrix NetScaler VPX-Appliance konfiguriert wird.

Task  | Beschreibung
------------- | -------------
[Zertifikat installieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-your-ssl-certificate) | Installieren Sie das SSL-Zertifikat, das Sie in der vorherigen [schrittweisen Anleitung](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx) erstellt  haben.
[DNS-Datensatz überprüfen und konfigurieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-check-and-configure-the-dns-record) | Stellen Sie sicher, dass ein DNS-Datensatz für den FQDN vorhanden ist, der auf die öffentliche Adresse verweist, die in Citrix NetScaler VPX als virtueller Server konfiguriert werden soll.
[Virtuellen SSL-Server hinzufügen und konfigurieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-add-and-configure-the-ssl-virtual-server) | Fügen Sie einen virtuellen SSL-Server hinzu und konfigurieren Sie ihn.
[Neue Cipher-Suite erstellen und anwenden](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-and-apply-a-new-cipher-suite) | Erstellen Sie eine Cipher-Suite, die AEAD, ECDHE und ECDSA priorisiert und bevorzugt.

## Zusätzliche Ressourcen
Die folgenden zusätzlichen Ressourcen können Ihnen dabei helfen, Citrix NetScaler VPX bei Verwendung des IBM Hardware Security Module bestmöglich zu nutzen.

* [Produktdokumentation zu NetScaler 12.1![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.citrix.com/en-us/netscaler/12-1/){:new_window}
* [Support-Portal zu Gemalto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://supportportal.gemalto.com/csm?id=csm_index){:new_window}
* [IBM Cloud-Support](https://{DomainName}/docs/get-support?topic=get-support-using-avatar){:new_window}
