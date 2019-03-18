---
copyright:
  years: 1994, 2017

lastupdated: "2018-08-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Reindirizzamento degli URL in un Citrix Netscaler VPX
{: #redirecting-urls-in-a-citrix-netscaler-vpx}

Il modo più comune per eseguire un reindirizzamento da `http://` a `https://` in NetScaler consiste nell'avvalersi della funzione di backup/reindirizzamento, che era stata originariamente concepita per eseguire un reindirizzamento a una pagina di "server inattivo" o "manutenzione".  

Per eseguire tale operazione, devi creare un server virtuale in ascolto sulla porta 80, sena alcun servizio effettivo associato a esso, e un reindirizzamento di backup a uno specifico URL `https://`. Il server virtuale effettivo è sempre "inattivo" (non è associato alcun servizio attivo) e, pertanto, il reindirizzamento di backup è sempre attivo. Lo svantaggio è che devi specificare un URL di reindirizzamento esplicito (ad esempio, `https://web.example.com`) e, di conseguenza, gli utenti che tentano di accedere a `http://mail.example.com` verrebbero reindirizzati a `https://web.example.com`.

Un metodo alternativo per eseguire un reindirizzamento per `http://` a `https://`, conservando al contempo nome host/URL fa uso della funzione "responder" di NetScaler, che crea un messaggio di reindirizzamento HTTP che include le informazioni originali. Tale operazione viene eseguita in pochi e semplici passi; nell'esempio di seguito, accertati di sostituire a "w.x.y.z" l'indirizzo IP del VIP HTTPS:

1. Prepara un tipo di monitor che avrà sempre esito positivo (il ping del localhost sarà sempre online finché NetScaler sarà attivo).
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```
	
2. Definisci un servizio fittizio con un IP che non verrà mai utilizzato (un indirizzo IP per un server a `1.1.1.1` che non sarà mai online).
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. Associa il servizio fittizio al monitor creato in precedenza per assicurarti che venga sempre notificato come attivo.
	```
	bind lb monitor localhost_ping Always_UP_service
	```
	
4. Fai in modo che NetScaler sia sempre in ascolto sulla porta 80 su un server virtuale, associandolo al servizio che rimarrà sempre attivo.
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```
	
5. Scrivi l'azione e la politica del responder per sostituire `http://` con `https://`.
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. Abilita la funzione responder del NetScaler (questo passo è cruciale, poiché la funzione è disabilitata per impostazione predefinita).
	```
        enable ns feature responder
	```
7. Associa il server virtuale in ascolto alla politica del responder.
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. Puoi confermare che sta funzionando come previsto utilizzando i programmi di utilità di riga di comando come ‘wget’ o ‘curl’ nel seguente modo:
        
	```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

    curl -v http://w.x.y.z
    ```

Sostituisci all'indirizzo IP `w.x.y.z` il nome host dell'URL (ad esempio, `http://mail.example.com` o `http://web.example.com`) e conferma che l'output “Location” rifletta lo stesso nome host che era stato specificato inizialmente, ma che inizia con “https”, come dagli esempi riportati di seguito:

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
