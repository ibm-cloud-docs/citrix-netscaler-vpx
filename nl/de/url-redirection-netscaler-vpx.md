---
copyright:
  years: 1994, 2017

lastupdated: "2018-08-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# URLs in Citrix NetScaler VPX weiterleiten
{: #redirecting-urls-in-a-citrix-netscaler-vpx}

Die am häufigsten verwendete Methode zur Durchführung einer Weiterleitung von `http://` an `https://` in NetScaler besteht in der Nutzung der Sicherungs- und Weiterleitungsfunktion, die ursprünglich für die Weiterleitung an eine Seite für einen Serverausfall oder eine Wartungsseite vorgesehen war.  

Hierzu müssen Sie einen virtuellen Server erstellen, der am Port 80 empfangsbereit ist und dem momentan keine Services über eine Bindung zugeordnet sind. Außerdem benötigen Sie eine Sicherungsweiterleitung an eine bestimmte `https://`-URL. Der eigentliche virtuelle Server ist immer "inaktiv" (keine Bindung zu Live-Services) und die Sicherungsweiterleitung demzufolge immer aktiv. Der Nachteil besteht darin, dass Sie eine explizite Weiterleitungs-URL (z. B. `https://web.example.com`) angeben müssen. Benutzer, die versuchen, auf `http://mail.example.com` zuzugreifen, werden an `https://web.example.com` weitergeleitet.

Eine alternative Methode zur Durchführung einer Weiterleitung von `http://` an `https://` bei gleichzeitiger Beibehaltung des Hostnamens und der URL besteht in der Verwendung der Responderfunktion von NetScaler. Diese Funktion erstellt eine HTTP-Weiterleitungsnachricht, die auch die Originalinformationen enthält. Hierzu werden einige einfache Schritte ausgeführt. Im folgenden Beispiel müssen Sie "w.x.y.z" durch die IP-Adresse der HTTPS-VIP ersetzen:

1. Bereiten Sie einen Überwachungstyp vor, der immer erfolgreich ausgeführt werden kann (beim Senden eines Pingsignals an den lokalen Host ist dieser immer im Onlinemodus, sofern NetScaler aktiv ist).
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```
	
2. Definieren Sie einen Fake-Service mit einer IP, die nie verwendet wird (IP-Adresse für einen Server unter `1.1.1.1`, der nie online ist).
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. Binden Sie den Fake-Service an die zuvor erstellte Überwachungsfunktion, um sicherzustellen, dass diese immer als aktiv gemeldet wird.
	```
	bind lb monitor localhost_ping Always_UP_service
	```
	
4. Definieren Sie NetScaler so, dass das System auf einem vserver immer am Port 80 empfangsbereit ist, und stellen Sie eine Bindung zu dem Service her, der immer aktiv bleibt.
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```
	
5. Schreiben Sie eine Responderaktion und -richtlinie zur Ersetzung von `http://` durch `https://`.
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. Aktivieren Sie die Responderfunktion für NetScaler (dieser Schritt ist von zentraler Bedeutung, da die Funktion standardmäßig inaktiviert ist).
	```
        enable ns feature responder
	```
7. Erstellen Sie eine Bindung des empfangsbereiten vservers an die Responderrichtlinie.
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. Sie können die ordnungsgemäße Funktion des Systems feststellen, indem Sie Befehlszeilendienstprogramme wie z. B. "wget" oder "curl" wie folgt verwenden:
        
	```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

    curl -v http://w.x.y.z
    ```

Ersetzen Sie die IP-Adresse `w.x.y.z` durch den URL-Hostnamen (z. B. `http://mail.example.com` oder `http://web.example.com`) und bestätigen Sie, dass die Ausgabe für den Standort ("Location") den gleichen Hostnamen angibt, der zu Beginn angegeben wurde, dass dieser jedoch wie in den folgenden Beispielen dargestellt mit "https" beginnt:

```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z
    --2012-06-18 08:42:20--  http://w.x.y.z/
    Connecting to w.x.y.z:80... connected.
    HTTP request sent, awaiting response...
      HTTP/1.1 302 Moved Temporarily
      Location: https://w.x.y.z/
      Connection: close
      Cache-Control: no-cache
      Pragma: no-cache

    wget  -S --max-redirect 0 -O /dev/null http://web.example.com
    --2012-06-18 08:42:20--  http://web.example.com/
    Connecting to w.x.y.z:80... connected.
    HTTP request sent, awaiting response...
      HTTP/1.1 302 Moved Temporarily
      Location: https://web.example.com/
      Connection: close
      Cache-Control: no-cache
      Pragma: no-cache

    wget  -S --max-redirect 0 -O /dev/null http://mail.example.com
    --2012-06-18 08:42:20--  http://mail.example.com/
    Connecting to w.x.y.z:80... connected.
    HTTP request sent, awaiting response...
      HTTP/1.1 302 Moved Temporarily
     Location: https://mail.example.com/
      Connection: close
      Cache-Control: no-cache
      Pragma: no-cache
```
