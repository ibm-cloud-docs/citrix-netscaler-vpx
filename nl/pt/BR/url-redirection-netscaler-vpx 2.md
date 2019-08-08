---
copyright:
  years: 1994, 2017

lastupdated: "2018-08-08"

keywords: redirect, url, monitor, responder

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Redirecionando URLs em um Citrix NetScaler VPX
{: #redirecting-urls-in-a-citrix-netscaler-vpx}

A maneira mais comum de executar um redirecionamento de `http://` para `https://` no NetScaler é aproveitar o recurso de backup/redirecionamento, destinado originalmente a redirecionar para uma página "servidor inativo" ou "manutenção".  

Para fazer isso, deve-se criar um servidor virtual que atenda na porta 80, sem serviços reais ligados a ele e um redirecionamento de backup para uma URL `https://` específica. O servidor virtual real está sempre "inativo" (sem serviços ligados em tempo real) e, portanto, o redirecionamento de backup está sempre ativo. A desvantagem é que se deve especificar uma URL de redirecionamento explícito (por exemplo, `https://web.example.com`) e, como resultado, os usuários que tentam acessar `http://mail.example.com` serão redirecionados para
`https://web.example.com`.

Um método alternativo para executar um redirecionamento de `http://` para `https://`, enquanto retém o nome do host/URL, usa o recurso "respondente" do NetScaler, que cria uma mensagem de redirecionamento de HTTP incluindo as informações originais. Isso é feito em algumas etapas simples - no exemplo abaixo certifique-se de substituir "w.x.y.z" pelo endereço IP do VIP HTTPS:

1. Prepare um tipo de monitor que sempre será bem-sucedido (a execução de ping do host local sempre estará on-line contanto que o NetScaler esteja ativo).
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```

2. Defina um serviço falso com um IP que nunca será usado (endereço IP para um servidor em `1.1.1.1` que nunca estará on-line).
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. Ligue o serviço falso ao monitor criado anteriormente para assegurar-se de que ele sempre seja relatado como ativo.
	```
	bind lb monitor localhost_ping Always_UP_service
	```

4. Faça com que o NetScaler sempre atenda na porta 80 em um vserver, ligando-o ao serviço que sempre permanecerá ativo.
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```

5. Grave a ação e a política do respondente para substituir `http://` por `https://`.
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. Ative o recurso de respondente do NetScaler (esta etapa é crucial, pois o recurso fica desativado por padrão).
	```
        enable ns feature responder
	```
7. Ligue o vserver de atendimento à política do respondente.
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. É possível confirmar que isso está funcionando conforme desejado usando os utilitários da linha de comandos, como 'wget' ou 'curl', conforme a seguir:

	```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

    curl -v http://w.x.y.z
    ```

Substitua o endereço IP `w.x.y.z` pelo nome do host da URL (por exemplo, `http://mail.example.com` ou `http://web.example.com`) e confirme se a saída “Local” reflete o mesmo nome do host que foi especificado inicialmente, mas iniciando com “https”, conforme os exemplos a seguir:

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
