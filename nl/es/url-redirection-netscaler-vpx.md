---
copyright:
  years: 1994, 2017

lastupdated: "2017-11-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Redirigir URL en un Citrix Netscaler VPX

La forma más común para realizar una redirección de `http://` a `https://` en NetScaler es aprovechar la característica de copia/redirección, que originalmente estaba destinada a redirigir a una página "servidor inactivo" o "mantenimiento".  

Para ello, debe crear una escucha de servidor virtual en el puerto 80, sin servicios reales vinculados, y una redirección de copia de seguridad a un determinado URL `https://`. El servidor virtual real está siempre "inactivo" (sin servicios enlazados) y, por lo tanto, la redirección de copia seguridad siempre está activa. El inconveniente es que debe especificar un URL de redirección explícito (por ejemplo, https://web.example.com), y como consecuencia, los usuarios que intenten acceder a http://mail.example.com serán redireccionados a https://web.example.com.

Un método alternativo para realizar una redirección de `http://` a `https://`, conservando el nombre de host/URL, utiliza la característica "respondedor" de NetScaler, que personaliza un mensaje de redirección de HTTP incluyendo la información original. Esto se realiza en unos sencillos pasos: en el ejemplo siguiente asegúrese de sustituir "w.x.y.z" con la dirección IP de la VIP de HTTPS:

1. Prepare un tipo de supervisor que siempre sea satisfactorio (el ping del sistema principal local siempre será en línea mientras NetScaler esté activo).
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```
	
2. Defina un servicio falso con una dirección IP que nunca se utilizará (dirección IP para un servidor en `1.1.1.1` que nunca estará en línea).
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. Enlace el servicio falsos con el supervisor creado anteriormente, para garantizar que siempre se informa como activo.
	```
	bind lb monitor localhost_ping Always_UP_service
	```
	
4. Haga que el NetScaler siempre escuche el puerto 80 en un servidor virtual enlazándolo con el servicio que siempre estará activo.
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```
	
5. Escriba la acción respondedor y la política para sustituir `http://` con `https://`.
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. Habilite la característica de respondedor de NetScaler (este paso es crucial, ya que la característica está inhabilitada de forma predeterminada).
	```
  enable ns feature responder
  ```
7. Enlace el servidor virtual que escucha con la política del respondedor.
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. Puede confirmar que funciona utilizando utilidades de línea de mandatos como 'wget' o 'curl' de la siguiente manera:

```
wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

curl -v http://w.x.y.z
```

Sustituya la dirección IP `w.x.y.z` para el nombre de host del URL (por ejemplo, http://mail.example.com o http://web.example.com) y confirme que la salida "Location" refleja el mismo nombre que ha especificado inicialmente, pero que empieza por "https" en los siguientes ejemplos:

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
