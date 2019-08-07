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

# IBM Hardware Security Module (HSM) mit {{site.data.keyword.vpx_full}} bereitstellen und konfigurieren
{: #deploying-and-configuring-the-ibm-hardware-security-module-hsm-with-citrix-netscaler-vpx}

Diese schrittweise aufgebaute Anleitung führt Sie durch die Integration des HSM in {{site.data.keyword.vpx_full}}. Die beiden Services werden dann in der Lage sein, miteinander zu kommunizieren und das für die Erstellung eines Zertifikats erforderliche Verschlüsselungsmaterial zu generieren.

## Informationen zur Bereitstellung
Diese Bereitstellung wurde mit den folgenden Komponentenspezifikationen erstellt und getestet:

| NetScaler VPX Version & Build	| HSM-Softwareversion | HSM-Firmwareversion | HSM-Clientversion |
| ------------- | ------------- | ------------- | ------------- |
| NS12.1: Build 48.13.nc | 6.2.2-5 | 6.10.9 | 6.2.2 |

**HINWEIS:** Wenn Ihre VPX-Version älter ist oder wenn bei der Bestellung der Einheit über die IBM© Cloud-Plattform nur Version 11.1 und frühere Versionen als Auswahloptionen angezeigt werden, kann ein Upgrade der Einheit durchgeführt werden, so dass die in dieser Anleitung beschriebene Konfiguration ausgeführt werden kann. 

## Logische Topologie
Das folgende Diagramm zeigt den Netzverkehrsdatenfluss für den Anwendungsfall 'SSL-Auslagerung'. Dieses Diagramm stellt eine visuelle und logische Perspektive des Trust-Links und der Konfiguration zwischen der VPX- und der HSM-Appliance bereit. 

<img src="images/network-flows-logical-topology.jpg" alt="Zeichnung" style="width: 700px;"/>

Wenn Sie mit der SSL-Auslagerung nicht vertraut sind, lesen Sie diesen [Citrix-Artikel](https://docs.citrix.com/en-us/netscaler/12-1/ssl.html).

## Durchgeführte Schritte

In dieser schrittweise aufgebauten Anleitung erfahren Sie, wie ein HSM mit einer {{site.data.keyword.vpx_full}}-Instanz bereitgestellt und konfiguriert wird.

Task  | Beschreibung
------------- | -------------
[IBM Hardware Security Module (HSM) bestellen](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-the-ibm-hardware-security-module-hsm-) | Zunächst müssen Sie ein HSM bestellen.
[{{site.data.keyword.vpx_full}} bestellen](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-a-citrix-netscaler-vpx) | Falls noch nicht geschehen, bestellen Sie einen {{site.data.keyword.vpx_full}}.
[HSM initialisieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-) | Bei den meisten Konfigurationen muss die HSM-Einheit initialisiert werden. Ohne Initialisierung können nur bestimmte `show`-Befehle ausgeführt werden. 
[Partition erstellen](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-a-partition) | Eine Partition ist ein logischer und unabhängiger Speicherbereich, der dem Client zugeordnet ist, der Verschlüsselungsobjekte in der HSM-Engine anfordert oder erstellt.
[HSM-Client-Software installieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-install-the-ibm-hardware-security-module-hsm-client-software) | In diesem Unterabschnitt wird VPX mit der Software und den Dienstprogrammen installiert, die für die Interaktion mit dem HSM erforderlich sind. |
[Network Trust Link (NTL) aufbauen](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-establish-a-network-trust-link-ntl-) | Ein Network Trust Link (NTL) ist ein sicherer Kanal für die Kommunikation zwischen dem Hardware Security Module (HSM) und dem Client. |
[Schlüssel erstellen und Zertifikatssignieranforderung generieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-) | In diesem Unterabschnitt wird beschrieben, wie ein Schlüsselpaar erstellt wird, das für die Generierung einer Zertifikatssignieranforderung (Certificate Signing Request, CSR) verwendet wird, und wie damit ein Zertifikat bestellt bzw. angefordert wird. | 
[Zertifikat bestellen](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-order-an-ssl-certificate) | Bestellen Sie ein SSL-Zertifikat für Ihren {{site.data.keyword.vpx_full}}.
[Zertifikat abrufen und übertragen](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-retrieve-and-transfer-the-certificate) | Rufen Sie das zuvor bestellte SSL-Zertifikat ab und bereiten Sie alles für seine Installation und Konfiguration in der nächsten Anleitung vor. 
