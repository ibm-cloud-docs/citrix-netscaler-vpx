---
copyright:
  years: 1994, 2018
  
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Neueste Aktualisierungen für Citrix NetScaler VPX
{: #recent-updates-for-citrix-netscaler-vpx}

## Version 12.1

### Virtuelle Server mit mehreren IP-Adressen
Sie können jetzt einen einzelnen virtuellen Lastausgleichsserver mit mehreren nicht fortlaufenden/fortlaufenden VIP-IPv4- und -IPv6-Adressen erstellen. Jede VIP-Adresse, die an einen virtuellen Server gebunden ist, wird als einzelner virtueller Server behandelt.

Weitere Informationen zu dieser Funktion finden Sie im Citrix-Artikel über [mehrere virtuelle IP-Server![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}.

### SSL
Die folgenden Aktualisierungen wurden für SSL-Verbindungen angewendet:
 
* Entfernen schwacher Chiffrierwerte aus der Chiffrierwertgruppe DEFAULT_BACKEND. 
* Unterstützung von ECDHE-Chiffrierwerten am Front-End des externen Thales nShield®-HSM.
* Unterstützung von ECDHE-Chiffrierwerten am Front-End des externen SafeNet-Netz-HSM.
* Entfernen von SSLv2: SSLv2 aus Release 12.1 wird von der NetScaler VPX-Appliance nicht unterstützt.

Weitere Informationen zu SSL-Aktualisierungen des Release 12.1 finden Sie in den [Releaseinformationen für Citrix 12.1![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}.

### Servicegruppenunterstützung für GSLB
Für GSLB (Global Server Load Balancing; globaler Serverlastausgleich) können Sie jetzt Servicegruppen konfigurieren, die auf IP-Adressen oder auf Domänennamen basieren, oder Servicegruppen mit automatischer Skalierung, die auf Domänennamen basieren. Darüber hinaus können Sie eine Servicegruppe genauso einfach wie einen einzelnen Service verwalten, eine Servicegruppe an einen virtuellen Server binden und der Gruppe Services hinzufügen.

Weitere Informationen zu GSLB-Servicegruppen finden Sie im Citrix-Artikel über die [Konfiguration einer GSLB-Servicegruppe![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}.
