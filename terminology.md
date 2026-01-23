---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-23"

keywords: nsip, snip, vip

subcollection: citrix-netscaler-vpx
---

{{site.data.keyword.attribute-definition-list}}

# Citrix Netscaler VPX terminology
{: #citrix-netscaler-vpx-terminology}

The {{site.data.keyword.vpx_full}} platform uses both product-specific terminology and basic load balancer terminology and concepts, many of which are defined here.
{: shortdesc}

## NetScaler IP (NSIP)
{: #netscaler-ip-nsip-}

The IP of the load balancer is designated for management purposes.

## SubNet IP (SNIP)
{: #subnet-ip-snip-}

A SNIP is the source IP address of a packet that is used by the NetScaler every time it wants to communicate with a server (or object). Servers also use the SubNet IP to respond to the NetScaler.

## Virtual IP (VIP)
{: #virtual-ip-vip-}

A VIP is an IP address to which a client sends requests. The NetScaler terminates the client connection at the VIP and then initiates a connection with a server that is configured in the load balancing service. This IP address can be either a public IP address for public (internet) traffic, or a private IP address for private (intranet) traffic.

## Virtual server
{: #virtual-server}

A virtual server refers to the combination of the IP address, port, and protocol to which an IP client connects. It also refers to where traffic requests are sent for a particular application that is being load-balanced by the NetScaler.

## Service
{: #service}

The combination of IP address, port, and protocol that is used to route requests to a specific server. A service, once configured, must later be associated to a virtual server.

## Server object
{: #server-object}

A virtual entity that enables you to assign a significant name to a physical server, rather than using its regular IP address.

## Monitor
{: #monitor}

An element that allows you to track a service, assuring that it is operating correctly. It uses probes and heartbeat signals to monitor the service status.
