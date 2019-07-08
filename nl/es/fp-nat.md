---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: nat, traffic, configure, configuration

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Configurar la conversión de direcciones de red de origen para el tráfico de salida
{: #configure-source-nat-for-outbound-traffic}

La conversión de direcciones de red (NAT) es un método para volver a correlacionar un espacio de dirección IP en otro modificando la información de direcciones de red en la cabecera de IP de los paquetes mientras están en tránsito a través de un dispositivo de direccionamiento de tráfico.

Puede utilizar el dispositivo Citrix NetScaler VPX para realizar una conversión de direcciones de red en el tráfico de salida desde las máquinas de cliente. Para ello, realice lo siguiente:

1. Vaya a Sistema > Red > Rutas y vaya al separador **RNAT**. Pulse **Configurar RNAT**.

2. Especifique la subred de origen (y la máscara) a la que desea aplicar RNAT y pulse **Aceptar**.

El tráfico enlazado a Internet procedente de cualquier IP de esta subred utilizará la conversión de direcciones de red para el tráfico en la dirección IP pública de Citrix NetScaler.    
