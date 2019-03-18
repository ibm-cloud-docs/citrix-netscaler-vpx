---

copyright:
  years: 2018
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# DNS-Datensatz überprüfen und konfigurieren
{: #check-and-configure-the-dns-record}

In diesem schrittweise aufgebauten Beispiel wird der DNS-Service von IBM© Cloud Internet Services für die Verwaltung der DNS-Zone und ihrer Datensätze verwendet. In diesem Fall müssen Sie sicherstellen, dass ein Datensatz für den verwendeten FQDN erstellt wird. Der DNS-Datensatz muss auf die öffentliche Adresse verweisen, die im virtuellen Server von Citrix NetScaler VPX konfiguriert werden soll.

<img src="images/12-add-record.png" alt="Zeichnung" style="width: 700px;"/>

Die statische öffentliche IP-Adresse, die für Citrix VPX verwendet werden soll, kann aus dem Kundenportal abgerufen werden. Navigieren Sie hierfür zu **Einheiten > Einheitenliste** und wählen Sie dann den Namen Ihrer Citrix NetScaler VPX-Instanz aus.

<img src="images/13-check-ip.png" alt="Zeichnung" style="width: 300px;"/>
