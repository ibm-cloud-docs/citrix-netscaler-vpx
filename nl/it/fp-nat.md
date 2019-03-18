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

# Configurazione del NAT di origine per il traffico in uscita
{: #configure-source-nat-for-outbound-traffic}

NAT (Network address translation) è un metodo di riassociazione di uno spazio di indirizzo IP in un altro modificando le informazioni dell'indirizzo di rete nell'intestazione IP dei pacchetti mentre transitano attraverso un dispositivo di instradamento del traffico.

Puoi utilizzare la tua applicazione Citrix NetScaler VPX per eseguire NAT sul traffico in uscita dalle tue macchine client. Per eseguire tale operazione:

1. Vai a System > Network > Routes e spostati nella scheda **RNAT**. Fai clic su **Configure RNAT**.

2. Specifica la sottorete di origine (e maschera) a cui desideri applicare RNAT e fai clic su **OK**.

Ora, il traffico verso Internet originato da un qualsiasi IP presente in questa sottorete utilizzerà NAT per il traffico sull'indirizzo IP pubblico di Citrix NetScaler.    
