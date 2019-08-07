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

# 在 {{site.data.keyword.vpx_full}} 中重定向 URL
{: #redirecting-urls-in-a-citrix-netscaler-vpx}

在 NetScaler 中执行 `http://` 到 `https://` 的重定向的最常见方法是利用备份/重定向功能，此功能最初旨在重定向到“服务器停止运行”或“维护”页面。  

要执行此操作，必须创建侦听端口 80 的虚拟服务器（未绑定任何实际服务），以及指向特定 `https://` URL 的备份重定向。实际虚拟服务器始终为“停止运行”（未绑定任何活动服务），因此备份重定向始终处于活动状态。缺点是必须指定显式重定向 URL（例如 `https://web.example.com`），因此尝试访问 `http://mail.example.com` 的用户将重定向到 `https://web.example.com`。

在保留主机名/URL 的同时执行 `http://` 到 `https://` 的重定向的替代方法是使用 NetScaler 的“响应者”功能，此功能生成包含原始信息的 HTTP 重定向消息。这可通过几个简单的步骤来完成 - 在以下示例中，请确保将“w.x.y.z”替换为 HTTPS VIP 的 IP 地址：

1. 准备将始终成功的监视器类型（只要 NetScaler 正在运行，对 localhost 执行 ping 操作的结果将始终为联机）。
	```
	Add lb monitor localhost_ping PING -LRTM ENABLED -destIP 127.0.0.1
	```

2. 使用永远不会使用的 IP 来定义一个伪服务（将永远不会联机的 IP 地址 `1.1.1.1` 用于服务器）。
	```
	Add service Always_UP_service 1.1.1.1 HTTP 80 -gslb NONE -maxClient 0 -maxReq 0 -cip ENABLED dummy -usip NO -sp OFF -cltTimeout 180 -svrTimeout 360 -CKA NO -TCPB NO -CMP YES
	```
3. 将伪服务绑定到先前创建的监视器，以确保该服务始终报告为“正在运行”。
	```
	bind lb monitor localhost_ping Always_UP_service
	```

4. 使 NetScaler 始终侦听 vserver 上的端口 80，并将其绑定到将始终保持运行的服务。
	```
	add lb vserver http_to_htps_vserver HTTP w.x.y.z 80 -timeout 0 -cltTimeout 180
	```
	```
	bind lb vserver http_to_htps_vserver Always_UP_service
	```

5. 编写响应者操作和策略，以将 `http://` 替换为 `https://`。
	```
	add responder action http_to_https_actn redirect "\"https://\" + http.req.hostname.HTTP_URL_SAFE + http.REQ.URL.PATH_AND_QUERY.HTTP_URL_SAFE"
	```
	```
	add responder policy http_to_https_pol HTTP.REQ.IS_VALID http_to_https_actn NOOP
	```
6. 启用 NetScaler 的响应者功能（此步骤非常重要，因为缺省情况下此功能已禁用）。
	```
        enable ns feature responder
	```
7. 将正在侦听的 vserver 绑定到响应者策略。
	```
	bind lb vserver http_to_htps_vserver -policyName http_to_https_pol -priority 1 -gotoPriorityExpression END
	```
8. 可以使用命令行实用程序（如“wget”或 "curl"）来确认它是否如预期正常运行，如下所示：

	```
    wget  -S --max-redirect 0 -O /dev/null http://w.x.y.z

    curl -v http://w.x.y.z
    ```

将 IP 地址 `w.x.y.z` 替换为 URL 主机名（例如，`http://mail.example.com` 或 `http://web.example.com`），并确认“Location”输出是否反映出最初指定的相同主机名，但在以下示例中各示例的“Location”均以“https”开头：

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
