---
copyright:
  years: 1994, 2017

lastupdated: "2018-08-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Redirecting URLs in a Citrix Netscaler VPX
{: #redirecting-urls-in-a-citrix-netscaler-vpx}

The most common way to perform a `http://` to `https://` redirect in NetScaler is to take advantage of the backup/redirect feature, which was originally intended to redirect to a "server down" or "maintenance" page.  

To do this, you must create a virtual server listening on port 80, with no actual services bound to it, and a back-up redirect to a specific `https://` URL. The actual virtual server is always “down” (no live services bound), and therefore the back-up redirect is always active. The drawback is that you must specify an explicit redirect URL (for example, `https://web.example.com`), and as a result, users attempting to access `http://mail.example.com` would get redirected to `https://web.example.com`.

An alternative method for performing a redirect for `http://` to `https://`, while retaining the hostname/URL, uses the "responder" feature of NetScaler, which crafts a HTTP redirect message including the original information. This is done in a few easy steps – in the below example be sure to replace "w.x.y.z" with the IP address of the HTTPS VIP:

1. Prepare a monitor type which will always succeed (pinging localhost will always be online as long as the NetScaler is up).
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```
	
2. Define a fake service with an IP that will never be used (IP address for a server at `1.1.1.1` which will never be online).
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. Bind the fake service to the previously created monitor, to ensure it is always reports as up.
	```
	bind lb monitor localhost_ping Always_UP_service
	```
	
4. Make the NetScaler always listen to port 80 on a vserver, binding it to the service that will always remain up.
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```
	
5. Write the responder action and policy to replace `http://` with `https://`.
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. Enable the responder feature of the NetScaler (this step is crucial, as the feature is disabled by default).
	```
        enable ns feature responder
	```
7. Bind the listening vserver to the responder policy.
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. You can confirm this is functioning as intended by using command-line utilities such as ‘wget’ or ‘curl’ as follows:
        
	```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

    curl -v http://w.x.y.z
    ```

Substitute the IP address `w.x.y.z` for the URL hostname (for example, `http://mail.example.com` or `http://web.example.com`) and confirm that the “Location” output reflects the same hostname which was initially specified, but starting with “https” per the following examples:

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