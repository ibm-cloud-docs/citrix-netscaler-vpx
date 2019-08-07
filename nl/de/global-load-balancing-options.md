---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Globaler Serverlastausgleich
{: #global-load-balancing}

Der globale Serverlastausgleich (GSLB = Global Server Load Balancing) stellt eine Methode dar, mit der der Datenverkehr auf mehrere Server aufgeteilt werden kann. Dazu werden ein DNS (Domain Name System) und die geografischen Standorte verwendet, um festzulegen, an welches Ziel der Serverdatenverkehr gesendet werden soll. Im Allgemeinen sendet eine Funktion für den globalen Lastausgleich eine Clientanforderung an den Server, der dem Client am nächsten liegt. Dadurch kann eine Reduzierung der Latenzzeiten und eine Verbesserung der Leistung erreicht werden.

Sie benötigen nicht unbedingt eine vollständige Implementierung einer globalen Lastausgleichslösung. Für GSLB sind mehrere Instanzen eines geeigneten Geräts erforderlich, das die Ausführung dieser Funktion unterstützt. Abhängig von Ihren individuellen Anforderungen können jedoch andere Lösungen geeigneter sein. Wenn Sie vollständige Websites und Anwendungen benötigen, dann stellt GSLB eine gute Wahl dar. Wenn Sie lediglich bestimmte Teile Ihrer Inhalte benötigen (z. B. Bilder, Videos oder andere große Dateien), dann ist ein [Content Delivery Network (CDN)](/docs/infrastructure/CDN?topic=CDN-about-content-delivery-networks-cdn-) möglicherweise die bessere (und einfacher bereitzustellende) Alternative.

## {{site.data.keyword.vpx_full}}

{{site.data.keyword.vpx_full}} stellt das einzige, vom Kunden konfigurierbare Gerät dar, mit dem ein echter globaler Lastausgleich durchgeführt werden kann. Bei NetScaler handelt es sich um eine multifunktionale Appliance, die Suchoperationen für den globalen Lastausgleich auf Basis eines DNS (Domain Name System) durchführen kann. Sie können das NetScaler-System als DNS-Server angeben. Das NetScaler-Gerät durchsucht in diesem Fall die Server, für deren Lastausgleich es konfiguriert wurde. Außerdem führt es eine Distanzberechnung durch und gibt einen Datensatz mit der IP des Servers zurück, der der Quelle der Clientanforderung am nächsten liegt.

Für den globalen Lastausgleich verwenden Sie eine NetScaler-Appliance-Konfiguration in jedem Rechenzentrum. Jede NetScaler-Appliance-Konfiguration kann - abhängig von den jeweiligen Anforderungen - aus einer einzelnen NetScaler-Instanz oder einem NetScaler-Paar in einem Hochverfügbarkeitspaar bestehen und damit lokale Lastausgleichservices für die zugrunde liegenden Server bereitstellen. Die Geräte sind so konfiguriert, dass sie miteinander kommunizieren und Statusinformationen für jeden Server austauschen können, der an dem Rotationsverfahren für den globalen Lastausgleich teilnimmt. Jede DNS-Anforderung, die auf den konfigurierten NetScaler-Systemen eingeht, kann einen korrekten Datensatz für einen Server zurückgeben, der online und reaktionsfähig ist. Alle Server, die nicht reagieren, werden aus dem Rotationszyklus entfernt und durch einen anderen Server ersetzt.

Die Lastausgleichsfunktion muss bereits konfiguriert sein. Dies gilt auch dann, wenn der Lastausgleich lediglich für einen Server durchgeführt wird. Für bestimmte Services benötigen Sie zusätzliche IP-Adressen. Dies gilt insbesondere für die IP der GSLB-Site. Diese IP wird von NetScaler zur Kommunikation mit anderen NetScaler-Systemen auf Basis des Protokolls für den globalen Lastausgleich verwendet. 

Die hier aufgeführte Prozedur für den globalen Lastausgleich verwendet die folgenden Komponenten:

### VPX1

`50.97.235.236` hat den Namen `VPX1Vserver` und stellt die lokale VIP (Virtual IP Address) für den Lastausgleich für dieses Gerät dar. `50.23.66.52` wird als `VPX1site` bezeichnet und stellt die lokale IP für den GSLB (Global Server Load Balancing) dieses Geräts dar.

### VPX2
`208.43.241.249` wird für `VPX2Vserver` verwendet und die GSLB-IP lautet `208.43.224.4`. Der Name ist `VPX2site`.

1. Rufen Sie die Optionen für **Datenverkehrsmanagement > GSLB** auf und klicken Sie mit der rechten Maustaste, um die Funktion zu aktivieren. Wählen Sie dann **Sites** und **Hinzufügen** aus.

2. Geben Sie auf dem ersten Gerät den Namen "VPX1", den Typ "Lokal" und die IP `50.23.66.52` ein und wählen Sie dann **Schließen** aus. 

	Nun wird die Site mit dem Status "Grün" aufgelistet. Fügen Sie noch keine ferne Site hinzu.

3. Rufen Sie die Optionen für **Datenverkehrsmanagement > GSLB** auf und wählen Sie dann den **GSLB-Assistenten** aus. Klicken Sie auf **Weiter**. Geben Sie den Namen des Hosts ein, für den der Lastausgleich durchgeführt werden soll (im vorliegenden Beispiel `gslb.tsstesting.com`). Übernehmen Sie den Datensatztyp "A" und den Servicetyp "ANY". Der Name des virtuellen Servers wird automatisch eingetragen. Klicken Sie auf **Weiter**.

4. Wählen Sie wie beim regulären Lastausgleich die gewünschte Lastausgleichs- und Persistenzmethode aus. Klicken Sie auf **Weiter**.

5. Die Site ist bereits eingetragen, sodass Sie keine weiteren Angaben hinzufügen müssen. Klicken Sie stattdessen auf das grüne Pluszeichen ("+") neben dem Namen der ersten Site. Wählen Sie den vserver dieses Geräts in der Liste aus und klicken Sie dann auf **Erstellen**. Die Site ist nun mit der Site-IP und der vserver-IP Ihrer Lastausgleichskonfiguration konfiguriert und grün markiert. Klicken Sie auf **Weiter**, **Fertigstellen** und **Beenden**.

6. Führen Sie die gleichen Aktionen für das nächste NetScaler-System aus und verwenden Sie dabei die Werte des entsprechenden Servers.

7. Wählen Sie auf beiden Servern die Optionen für **Datenverkehrsmanagement > DNS > Datensätze > A-Datensätze** aus und prüfen Sie die Liste. Sie muss die Einträge für `root.servers.net` und außerdem Ihren Hostnamen sowie den Typ "GSLB DOMAIN" enthalten. 

8. Rufen Sie die Optionen für **Datenverkehrsmanagement > DNS > Namensserver** auf und klicken Sie dann auf **Hinzufügen**. Geben Sie eine IP-Adresse auf dem NetScaler-System (z. B. die öffentliche IP-Adresse des Geräts) ein. Klicken Sie auf **Lokal** und übernehmen Sie das Protokoll "UDP". Klicken Sie auf **Erstellen** und dann auf **Schließen**. Daraufhin wird der geltende Status als aktiviert und betriebsbereit angezeigt.

9. Rufen Sie die Optionen für **System > Netz > IPs** auf und öffnen Sie die GSLB-IP-Adresse. Vergewissern Sie sich, dass für beide Maschinen die Einstellung **Management** ausgewählt ist.

10. Rufen Sie dann auf beiden Servern erneut die Optionen für **Datenverkehrsmanagement > GSLB** auf und durchlaufen Sie den Assistenten erneut. Klicken Sie dieses Mal auf **Weiter** und wählen Sie dann die Option zur **Änderung der Konfiguration für vorhandene Domänen** aus. Wählen Sie in der Liste den Hostnamen aus und klicken Sie dann zwei Mal auf **Weiter**. 

11. Geben Sie im Feld für die Siteadresse die IP-Adresse der Site für das andere NetScaler-System ein. Ordnen Sie ihm den Namen der Site des anderen NetScaler-Systems zu und klicken Sie dann auf **Hinzufügen**. Daraufhin erscheint für die Site eine Option zum erneuten Klicken auf das grüne Pluszeichen ("+"). Klicken Sie auf das Pluszeichen der fernen Site, um eine weitere Site hinzuzufügen. Geben Sie die IP des vserver-Service (für die Server mit Lastausgleich, nicht die IP der GSLB-Site) und den Port ein. Klicken Sie dann auf **Erstellen** und **Schließen**, **Weiter**, **Fertigstellen** und anschließend auf **Beenden**.

Sofern bislang keine Probleme aufgetreten sind und beide Server konfiguriert wurden, haben sämtliche Komponenten in den virtuellen GSLB-Servern sowie den entsprechenden Services und Sites den Status "Grün". Sie werden feststellen, dass in den GSLB-Services zwei Einträge auf beiden Maschinen vorhanden sind, wenn diese korrekt synchronisiert wurden. Die Server kommunizieren nun miteinander.

Als nächsten Schritt müssen Sie nun das DNS (Domain Name System) konfigurieren.

Im vorliegenden Beispiel (`gslb.tsstesting.com`) erstellen Sie "NS" und ordnen in der Zone "tsstesting.com" Datensätze zu:

    gslb.tsstesting.com. IN NS NS1.gslb.tsstesting.com
    gslb.tsstesting.com. IN NS NS2.gslb.tsstesting.com
    NS1.gslb.tsstesting.com. IN A 10.54.0.141 ; nameserver IP of first NetScaler
    NS2.gslb.tsstesting.com. IN A 172.16.1.101 ; nameserver IP of second NetScaler
    www.tsstesting.com. IN CNAME gslb.tsstesting.com ; alias to the GSLB object on the NetScaler appliance

Beachten Sie hierbei, dass Sie CNAMEs nur mit Hostnamen, nicht jedoch mit dem Rootelement der Domäne verwenden können.

Mit dieser Konfiguration werden die Namensserver für `gslb.tsstesting.com`-Anforderungen an die NetScaler-IPs eingerichtet, für die Sie das DNS konfiguriert haben. Der CNAME-Datensatz übersetzt `tsstesting.com` in eine Anforderung für `gslb.tsstesting.com`. Alle Anforderungen für `www.tsstesting.com` werden dann zur Auflösung an NetScaler übertragen und geben einen Datensatz zurück, der auf Basis der von Ihnen konfigurierten Lastausgleichsmethode ermittelt wird.

Weitere Informationen zum globalen Lastausgleich mit NetScaler finden Sie in den Quellen zu folgenden Themen:
* [Konfiguration von NetScaler für den globalen Lastausgleich ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://support.citrix.com/article/CTX110348){: new_window}
* [Funktionsweise des DNS (Domain Name System) mit der GSLB-Funktion unter NetScaler ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://support.citrix.com/article/CTX122619){: new_window}
* [Informationen zum MEP-Protokoll und zur Siteüberwachung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://support.citrix.com/article/CTX111081){: new_window}

Es stehen auch andere Produkte mit ähnlicher Funktionalität zur Verfügung, mit denen der Datenverkehr auf verschiedene geografische Regionen verteilt werden kann:

### CDN

Netze zur Bereitstellung von Inhalten (CDNs = Content Delivery Networks) ermöglichen Ihnen das Hochladen oder Bereitstellen eines Ursprungsservers auf geografisch verteilte(n) Cache-Server(n). Diese können anschließend zur Bereitstellung der Inhalte für die anfordernden Clients genutzt werden. CDNs eignen sich am besten für statische Masseninhalte wie beispielsweise Bilder und Videos, die sich im Zeitverlauf nicht ändern.

Weitere Einzelheiten zu CDNs finden Sie in [dieser Dokumentation](/docs/infrastructure/CDN?topic=CDN-getting-started).

### Objektspeicher

Der Objektspeicher von {{site.data.keyword.BluSoftlayer_notm}} kann zur Verwendung verschiedener geografischer Standorte in unterschiedlichen Rechenzentren konfiguriert werden, um Inhalte bereitzustellen. Eine Anwendung, bei der geografische Gegebenheiten berücksichtigt werden, kann zur Durchführung standortbasierter Suchoperationen für Clientanforderungen und zur Rückgabe einer URL an den Objektspeicher in Clientnähe verwendet werden. Der Objektspeicher umfasst außerdem eine CDN-Front-End-Komponente, die bei Bedarf zur Bereitstellung zusätzlicher Caching-Services (siehe oben) genutzt werden kann.

Weitere Informationen sowie eine Einführung zum Objektspeicher finden Sie in [dieser Dokumentation](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-about-ibm-cloud-object-storage). 
