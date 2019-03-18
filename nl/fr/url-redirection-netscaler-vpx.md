---
copyright:
  years: 1994, 2017

lastupdated: "2018-08-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Redirection d'URL dans un Citrix NetScaler VPX
{: #redirecting-urls-in-a-citrix-netscaler-vpx}

Le moyen le plus courant d'effectuer une redirection de `http://` vers `https://` dans NetScaler est de tirer parti de la fonctionnalité de secours/redirection, qui était prévue à l'origine pour rediriger l'utilisateur vers une page l'informant que le serveur est en panne ou en maintenance.  

Pour ce faire, vous devez créer un serveur virtuel écoutant sur le port 80, sans lui associer aucun service, ainsi qu'une redirection de secours vers une URL `https://` spécifique. Le serveur virtuel proprement dit est toujours “hors service” (aucun service “live” ne lui est associé) et, par conséquent, la redirection de secours est toujours active. L'inconvénient est que vous devez spécifier une URL de redirection explicite (par exemple, `https://web.example.com`). Cela signifie que les utilisateurs tentant d'accéder à `http://mail.example.com` seront systématiquement redirigés vers `https://web.example.com`.

Une autre méthode de redirection de `http://` vers `https://`, qui cette fois conserve le nom d'hôte/l'URL spécifiés initialement, consiste à utiliser la fonction "répondeur" de NetScaler, laquelle fabrique un message de redirection HTTP incluant les informations d'origine. Sa mise en oeuvre ne nécessite que quelques étapes simples.
Dans l'exemple suivant, pensez à remplacer "w.x.y.z" par l'adresse IP virtuelle (VIP) HTTPS :

1. Préparez un type de moniteur qui obtienne toujours une réponse positive (un ping à localhost réussira toujours aussi longtemps que le NetScaler sera en fonctionnement).
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```
	
2. Définissez un service factice, ayant une IP qui ne sera jamais utilisée (adresse IP d'un serveur à `1.1.1.1` qui ne sera jamais en ligne).
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. Liez le service factice au moniteur créé précédemment afin qu'il soit toujours signalé comme actif.
	```
	bind lb monitor localhost_ping Always_UP_service
	```
	
4. Faites en sorte que le NetScaler écoute toujours le port 80 sur un serveur virtuel (vserver) et liez ce dernier au service toujours actif (Always_UP_service).
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```
	
5. Ecrivez l'action du répondeur et la politique associée visant à remplacer `http://` par `https://`.
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. Activez la fonctionnalité répondeur du NetScaler (cette étape est primordiale, car la fonctionnalité répondeur est désactivée par défaut).
	```
        enable ns feature responder
	```
7. Liez le serveur virtuel en mode écoute à la politique du répondeur.
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. Vous pouvez à présent vérifier que tout fonctionne comme prévu en utilisant un utilitaire de ligne de commande tel que ‘wget’ ou ‘curl’ comme suit :
        
	```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

    curl -v http://w.x.y.z
    ```

Remplacez l'adresse IP `w.x.y.z` par le nom d'hôte sous forme d'URL (par exemple, `http://mail.example.com` ou `http://web.example.com`) et vérifiez que la sortie “Location” reflète bien le nom d'hôte spécifié initialement, mais commençant par “https”, comme dans les exemples ci-dessous :

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
