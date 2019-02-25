---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX Terminology
{: #citrix-netscaler-vpx-terminology}

The Citrix NetScaler platform uses both product-specific terminology and basic load balancer terminology and concepts. 

### NetScaler IP (NSIP)

The IP of the load balancer designated for management purposes.

### SubNet IP (SNIP)

A SNIP is the source IP address of a packet used by the NetScaler every time it wants to communicate with a server (or object). Servers also use the SubNet IP to respond to the NetScaler.

### Virtual IP (VIP)

A VIP is an IP address to which a client sends requests. The NetScaler terminated the client connection at the VIP and then initiates a connection with a server configured in the load balancing service.  This can be either a public IP address for public (internet) traffic, or a private IP address for private (intranet) traffic.

### Virtual Server

A Virtual Server, in load balancing terms, refers to the combination of the IP address, port, and protocol to which an IP client connects and where traffic requests are sent for a particular application that is being load-balanced by the NetScaler.

### Service

The combination of IP address, port, and protocol used to route requests to a specific server. A Service, once configured, must later be associated to a Virtual Server.

### Server Object

A virtual entity that enables you to assign a significant name to a physical server, rather than using its regular IP address.

### Monitor

An element that allows you to track a service, assuring that it is operating correctly. The monitor uses probes and heartbeat signals to keep track of the Service status.