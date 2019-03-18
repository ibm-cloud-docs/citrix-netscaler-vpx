---
copyright:
  years: 1994, 2018
  
lastupdated: "2018-11-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Actualizaciones recientes de Citrix NetScaler VPX
{: #recent-updates-for-citrix-netscaler-vpx}

## Versión 12.1

### Servidores virtuales con varias direcciones IP
Ahora puede crear un servidor virtual de equilibrio de carga único con varias direcciones IPv6 e IPv4 VIP consecutivas/no consecutivas. Cada dirección VIP enlazada a un servidor virtual se trata como un servidor virtual individual.

Para obtener más información sobre esta característica, consulte el artículo de Citrix [Varios servidores virtuales IP ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.citrix.com/en-us/netscaler/12-1/load-balancing/load-balancing-customizing/multi-ip-virtual-servers.html){: new_window}.

### SSL
Se han aplicado las actualizaciones siguientes para las conexiones SSL:
 
* Eliminación de cifrados débiles del grupo de cifrado DEFAULT_BACKEND. 
* Soporte para los cifrados ECDHE en el frontal del HSM externo de Thales nShield®
* Soporte para los cifrados ECDHE en el frontal del HSM externo de la red de SafeNet
* Eliminación de SSLv2: El dispositivo NetScaler VPX no ofrece soporte a SSLv2 a partir del release 12.1.

Para obtener más detalles sobre las actualizaciones de SSL 12.1, consulte las [notas de la versión de Citrix 12.1 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.citrix.com/en-us/netscaler/12-1/downloads/release-notes-12-1-48-13.html){: new_window}.

### Soporte de grupos de servicio para GSLB
Ahora puede configurar grupos de servicio basados en direcciones IP, grupos de servicio basados en nombres de dominio o grupos de servicios de escalado automático basados en nombres de dominio para GSLB. También puede gestionar un grupo de servicios de forma tan sencilla como un único servicio y enlazar un grupo de servicios a un servidor virtual, así como añadir servicios al grupo.

Para obtener más información sobre los grupos de servicio de GSLB, consulte el artículo de Citrix [Configuración de un grupo de servicios GSLB ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.citrix.com/en-us/netscaler/12/global-server-load-balancing/configure/configuring-a-gslb-service-group.html){: new_window}.
