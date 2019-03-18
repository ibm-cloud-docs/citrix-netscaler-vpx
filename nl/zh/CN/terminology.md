---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX 术语
{: #citrix-netscaler-vpx-terminology}

Citrix NetScaler 平台使用特定于产品的术语以及基本负载均衡器的术语和概念。 

### NetScaler IP (NSIP)

为管理目的而指定的负载均衡器的 IP。

### 子网 IP (SNIP)

SNIP 是 NetScaler 每次需要与服务器（或对象）通信时使用的包的源 IP 地址。服务器还使用子网 IP 来响应 NetScaler。

### 虚拟 IP (VIP)

VIP 是客户机向其发送请求的 IP 地址。NetScaler 会终止 VIP 上的客户机连接，然后启动与负载均衡服务中所配置的服务器的连接。这可以是用于公共（因特网）流量的公共 IP 地址，也可以是用于专用（内部网）流量的专用 IP 地址。

### 虚拟服务器

在负载均衡术语中，虚拟服务器是指 IP 客户机连接到的 IP 地址、端口和协议的组合，并可通过该组合针对正在由 NetScaler 负载均衡的特定应用程序发送流量请求。

### 服务

用于将请求路由到特定服务器的 IP 地址、端口和协议的组合。服务一旦配置后，必须稍后与虚拟服务器相关联。

### 服务器对象

一个虚拟实体，支持向物理服务器分配有效名称，而不使用其常规 IP 地址。

### 监视器

一个元素，支持跟踪服务，确保该服务正常运行。监视器使用探测器和脉动信号来跟踪服务状态。
