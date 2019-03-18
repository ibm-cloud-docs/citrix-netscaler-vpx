---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Citrix NetScaler VPX-Terminologie
{: #citrix-netscaler-vpx-terminology}

Auf der Citrix NetScaler-Plattform werden sowohl die produktspezifische Terminologie als auch die grundlegenden Begriffe und Konzepte zum Lastausgleich verwendet. 

### NetScaler-IP (NSIP)

Die IP der Lastausgleichsfunktion, die zu Managementzwecken vorgesehen ist.

### Teilnetz-IP (SNIP)

Eine SNIP (Subnet IP; Teilnetz-IP) ist die Quellen-IP-Adresse eines Pakets. Sie wird von NetScaler verwendet, wenn mit einem Server (oder Objekt) kommuniziert werden soll. Server verwenden die Teilnetz-IP außerdem zum Senden von Antworten an NetScaler.

### Virtuelle IP (VIP)

Eine VIP ist eine IP-Adresse, an die ein Client Anforderungen sendet. NetScaler hat die Clientverbindung an der VIP beendet und stellt dann eine Verbindung zu einem Server her, der im Lastausgleichsservice konfiguriert wurde.  Hierbei kann es sich entweder um eine öffentliche IP-Adresse für den öffentlichen Datenverkehr (Internet) oder um eine private IP-Adresse für den privaten Datenverkehr (Intranet) handeln.

### Virtueller Server

Ein virtueller Server stellt im Kontext des Lastausgleichs eine Kombination aus der IP-Adresse, dem Port und dem Protokoll dar, mit deren Hilfe ein IP-Client eine Verbindung herstellt und über die Datenverkehrsanforderungen für eine bestimmte Anwendung gesendet werden, für die über NetScaler ein Lastausgleich durchgeführt wird.

### Service

Die Kombination aus IP-Adresse, Port und Protokoll, die zur Weiterleitung von Anforderungen an einen bestimmten Server verwendet wird. Ein Service muss nach seiner Konfiguration einem virtuellen Server zugeordnet werden.

### Serverobjekt

Eine virtuelle Entität, die Ihnen die Möglichkeit bietet, einem physischen Server einen signifikanten Namen zuzuordnen, anstatt seine reguläre IP-Adresse zu verwenden.

### Überwachungsfunktion

Eine Funktion, die Ihnen die Verfolgung eines Service erlaubt und sicherstellt, dass dieser Service ordnungsgemäß arbeitet. Die Überwachungsfunktion verwendet Testmonitore und Überwachungssignale, um den Servicestatus zu verfolgen.
