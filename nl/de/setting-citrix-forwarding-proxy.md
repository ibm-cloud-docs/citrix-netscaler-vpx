---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.vpx_full}} als Weiterleitungsproxy konfigurieren
{: #setting-up-citrix-netscaler-vpx-as-a-forwarding-proxy}

Ein Weiterleitungsproxy fungiert als zentraler Steuerungspunkt zwischen Clients in einem internen Netz und dem Internet. Ein Proxy ermöglicht dem Netz- oder Sicherheitsadministrator die Erstellung von Richtlinien, die den Zugriff auf Internet-Sites einschränken.

Wenn ein Client im internen Netz eine Anforderung absetzt, dann wird die IP-Adresse des Proxys verwendet, um die Anforderung an den fernen Server im Internet zu übergeben. Der ferne Server sendet daraufhin eine Antwort an den Proxy, der seinerseits die Antwort an den Client zurückgibt.

Normalerweise wird ein Proxy mit einer Firewall kombiniert, um die Sicherheit der Clients in einem internen Netz zu gewährleisten.

## Schritt 1: Zu verwendende VIPs im privaten Netz anfordern 

Wenn eine {{site.data.keyword.vpx_full}}-Lastausgleichsfunktion im Kundenportal von {{site.data.keyword.BluSoftlayer_notm}} bestellt wird, dann wird angenommen, dass ein Reverse Proxy angefordert wird. Der Anforderer wird zur Angabe der Anzahl der öffentlichen IPs aufgefordert, die als virtuelle IPs (VIPs) benutzt werden sollen.

Im Falle eines Forward Proxys müssen die VIPs in einem privaten Netz eingerichtet werden. Es muss ein Support-Ticket geöffnet werden, um VIPs für das private Netz anzufordern. Die erforderliche Anzahl der VIPs bestimmt die Größe des Teilnetzes, die im Ticket angefordert wird. Die Teilnetzinformationen werden im Ticket zurückgegeben.

Im vorliegenden Beispiel wurde ein Teilnetz vom Typ `/29` angefordert. Dadurch ergibt sich Folgendes:

* Erstellung des Teilnetzes `10.114.27.0/29` zur Verwendung als private VIPs.

* Teilnetz-IP (SNIP) `10.114.52.101` und weitergeleitetes Teilnetz `10.114.27.0/29`.

* Die VIPs `10.114.27.0-3` wurden vom Support-Team zu {{site.data.keyword.vpx_full}} hinzugefügt.

## Schritt 2: Lastausgleichs- und Cacheweiterleitungsfunktionen für {{site.data.keyword.vpx_full}} aktivieren

Standardmäßig sind die Lastausgleichs- und Cacheweiterleitungsfunktionen für die {{site.data.keyword.vpx_full}}-Einrichtung für den Lastausgleich inaktiviert. Diese Funktionen können mit dem Befehl `enable ns feature cr lb` aktiviert werden.


## Schritt 3: Forward Proxy erstellen

Geben Sie in der Befehlszeile die folgenden Befehle für {{site.data.keyword.vpx_full}} ein. Im vorliegenden Szenario wird lediglich einer der beiden DNS-Server für {{site.data.keyword.BluSoftlayer_notm}} hinzugefügt.  

```
add cr vserver vs_forward_cache HTTP 10.114.27.3 80 -cachetype forward -redirect origin

add lb vserver virtual_dns DNS 10.114.27.4 53

add service Real_DNSServer 10.0.80.12 DNS 53

bind lb vserver virtual_dns Real_DNS

set cr vserver vs_forward_cache -dnsVservername virtual_dns
```

Mit dem Befehl in Zeile 1 wird der Weiterleitungscache erstellt. Als Protokoll wird HTTP verwendet und `10.114.27.3` stellt eine der VIPs dar, die im privaten Netz angefordert wurden. Als Port wird der Standardport 80 für HTTP verwendet. Da diese Kombination aus Adresse und Port als Proxyanweisung im Browser verwendet wird, kann der Port beliebig geändert werden.

In Zeile 2 wird eine Lastausgleichs-VIP hinzugefügt, die für das "reale" DNS steht.

In Zeile 3 wird die IP-Adresse des "realen" DNS als Service hinzugefügt. Diese Adresse kann das Kunden-DNS angeben oder es kann eine Weiterleitung zurück an die DNS-Auflöser durchgeführt werden, die von {{site.data.keyword.BluSoftlayer_notm}} bereitgestellt werden.

Zeile 4 stellt eine Bindung zwischen der VIP und dem "realen" Server her. Alle DNS-Anforderungen für `10.114.27.4` werden an `10.0.80.12` gesendet.

Zeile 5 weist den virtuellen Server des Weiterleitungsproxys an, zur Namensauflösung das virtuelle DNS zu verwenden.

## Client konfigurieren

Bevor die Anpassung des Clients zur Verwendung des Weiterleitungsproxys fortgesetzt wird, sollten Sie sich vergewissern, dass keine öffentliche Site (z. B. http://www.ibm.com) erreicht werden kann. Verwenden Sie dazu den Browser Firefox auf dem Client. Da auf dem Client keine öffentliche Schnittstelle vorhanden sein darf, muss diese Anforderung fehlschlagen. 

Im folgenden Beispiel wird ein Linux-Client konfiguriert.

Am Client müssen einige Änderungen durchgeführt werden. Mit der ersten Änderung muss ein Zeiger erstellt werden, mit dem vom Auflöser des Clients auf das virtuelle DNS verwiesen wird. Hierzu können Sie wie folgt vorgehen.

Sie können die Datei `/etc/resolv.conf` manuell bearbeiten und dabei den Verweis auf die virtuelle Adress des DNS angeben. Beachten Sie dabei, dass die Tools für die Clientverwaltung diese Änderungen möglicherweise wieder auf die ursprünglichen Einstellungen zurücksetzen.  

Alternativ hierzu können Sie die Schnittstelle `/etc/sysconfig/network-scripts/ifcfg-ethx` bearbeiten und die Anweisung `DNS1=` hinzufügen. Nachdem diese Einstellung angegeben wurde, kann der Servicebefehl für den Neustart des Netzes ausgegeben werden, um die Änderungen zu aktivieren.

In beiden Fällen muss die DNS-IP-Adresse als virtuelle DNS-Adresse konfiguriert werden und der Browser des Clients muss so konfiguriert werden, dass Anforderungen an den Weiterleitungsproxy von {{site.data.keyword.vpx_full}} übergeben werden.

Führen Sie die folgenden Schritte in Firefox aus, um die erforderlichen Änderungen durchzuführen:

1. Klicken Sie auf die Optionen für **Einstellungen > Erweitert > Netz > Netzverbindungseinstellungen**.

* Wählen Sie die Option für die **manuelle Proxy-Konfiguration** aus und geben Sie dann Folgendes ein:

  * **Adresse:** 10.114.27.3

  * **Port:** 80

  * Aktivieren Sie das Kontrollkästchen für die **Verwendung dieses Proxy-Servers für alle Protokolle**.

* Klicken Sie auf **Speichern** und schließen Sie das Browserfenster.

Die IP-Adresse `10.114.27.3` ist die IP-Adresse des Weiterleitungscaches, der in Schritt 1 erstellt wurde.

Die Konfiguration ist nun abgeschlossen und Sie können über die im privaten Netz isolierte Ressource auf das Internet zugreifen.

## Konfiguration überprüfen

Nach der Konfiguration des Clients zur Verwendung des Weiterleitungsproxys sollten Sie erneut versuchen, auf die öffentliche Site zuzugreifen. Nun muss diese Anforderung erfolgreich ausgeführt werden.

Die folgenden Anzeigebefehle können verwendet werden, um den Status des Weiterleitungsproxys zu überprüfen.

**show cr policy:** Zeigt alle vorhandenen Richtlinien für die Cacheweiterleitung an.

**show policy map:** Zeigt die konfigurierten Zuordnungsrichtlinien und die zugehörigen Zuordnungsrichtlinieninformationen an.

**show cr vserver:** Zeigt einen angegebenen virtuellen Server für die Cacheweiterleitung oder alle konfigurierten virtuellen Server für die Cacheweiterleitung an.

**stat cr vserver:** Zeigt die vserver-Statistik für die Cacheweiterleitung an.

Die Konfiguration eines grundlegenden Weiterleitungsproxys unter Citrix ist relativ einfach. Sie bietet Clients in einem internen Netz eine sichere Möglichkeit für den Zugriff auf Ressourcen im Internet. Außerdem ermöglicht sie dem Netzadministrator die Beibehaltung eines gewissen Grads an Kontrolle über das Netz.

Bei der Implementierung am Kundenstandort sollte eine Firewall zur Konfiguration hinzugefügt werden, um die Ressourcen weiter zu schützen.
