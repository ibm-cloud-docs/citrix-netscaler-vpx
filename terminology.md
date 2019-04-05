---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"

keywords: terminology, nsip, snip, vip, service, object, monitor

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Citrix NetScaler VPX Terminology
{: #citrix-netscaler-vpx-terminology}

The Citrix NetScaler platform uses both product-specific terminology and basic load balancer terminology and concepts.

### NetScaler IP (NSIP)
{: #netscaler-ip-nsip-}

The IP of the load balancer designated for management purposes.

### SubNet IP (SNIP)
{: #subnet-ip-snip-}

A SNIP is the source IP address of a packet used by the NetScaler every time it wants to communicate with a server (or object). Servers also use the SubNet IP to respond to the NetScaler.

### Virtual IP (VIP)
{: #virtual-ip-vip-}

A VIP is an IP address to which a client sends requests. The NetScaler terminated the client connection at the VIP and then initiates a connection with a server configured in the load balancing service.  This can be either a public IP address for public (internet) traffic, or a private IP address for private (intranet) traffic.

### Virtual Server
{: #virtual-server}

A Virtual Server, in load balancing terms, refers to the combination of the IP address, port, and protocol to which an IP client connects and where traffic requests are sent for a particular application that is being load-balanced by the NetScaler.

### Service
{: #service}

The combination of IP address, port, and protocol used to route requests to a specific server. A Service, once configured, must later be associated to a Virtual Server.

### Server Object
{: #server-object}

A virtual entity that enables you to assign a significant name to a physical server, rather than using its regular IP address.

### Monitor
{: #monitor}

An element that allows you to track a service, assuring that it is operating correctly. The monitor uses probes and heartbeat signals to keep track of the Service status.
