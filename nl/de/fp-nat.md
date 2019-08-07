---



copyright:
  years: 2017
lastupdated: "2018-11-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Quellen-NAT für abgehenden Datenverkehr konfigurieren
{: #configure-source-nat-for-outbound-traffic}

Bei der Netzadressumsetzung (Network Address Translation; NAT) handelt es sich um eine Methode zur Neuzuordnung eines IP-Adressraums in einen anderen Adressraum. Hierbei werden Netzadressinformationen im IP-Header von Paketen während ihres Wegs in einer Datenverkehrs-Routing-Einheit geändert.

Sie können Ihre {{site.data.keyword.vpx_full}}-Appliance für die Netzadressumsetzung im abgehenden Datenverkehr von Ihren Clientmaschinen verwenden. Gehen Sie hierfür wie folgt vor:

1. Klicken Sie auf 'System > Netz > Routen' und navigieren Sie zur Registerkarte **RNAT**. Klicken Sie auf **RNAT konfigurieren**.

2. Geben Sie das Quellenteilnetz (und die Teilnetzmaske) an, auf das RNAT angewendet werden soll, und klicken Sie auf **OK**.

Der internetgerichtete Datenverkehr, der aus einer beliebigen IP-Adresse in diesem Teilnetz stammt, verwendet jetzt NAT für den Datenverkehr über die öffentliche IP-Adresse von Citrix NetScaler.    
