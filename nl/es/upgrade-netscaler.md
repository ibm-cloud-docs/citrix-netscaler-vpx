---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: upgrade, vpx, callhome

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Actualización de Citrix NetScaler VPX
{: #upgrading-your-citrix-netscaler-vpx}

Debe estar conectado a la VPN antes de intentar este procedimiento.
{: note}

1. Inicie sesión en la IP de gestión de NetScaler.
2. Pulse **Actualización del sistema**.
4. Seleccione **Local** desde la lista desplegable **Elegir archivo**.
4. Descargue el archivo de actualización correcto desde la siguiente ubicación:

	[Versiones disponibles de NetScaler ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}

	Debe estar conectado a la VPN de IBM© Cloud Infrastructure para acceder a este enlace.
  {: note}

5. En la pantalla Actualizar software, vaya a la ubicación del archivo de actualización y pulse **Actualizar**. El firmware se actualizará.
6. En la ventana Actualización del sistema resultante, se le solicitará que rearranque. Pulse **Cerrar**.
7. Vuelva a **Sistema**, y pulse **Rearrancar**.
8. Después de la actualización, cierre todas las instancias de navegador y borre la memoria caché del sistema antes de acceder al dispositivo.


La interfaz de usuario puede diferir dependiendo de la versión actual del NetScaler VPX.
{: note}

Si está actualizando de NetScaler versión 11 a la 12, la característica CallHome se habilita de forma predeterminada, incluso si la inhabilita específicamente antes y durante la instalación. Para inhabilitar esta característica, puede utilizar esta línea de mandatos o la IU de gestión de Citrix:

   * Línea de mandatos: `disable feature CallHome`
   * IU de gestión de Citrix:

     1. Vaya a **Configuración** > **Sistema** > **Valores**.
     2. En el panel de detalles, pulse el enlace **Configurar características avanzadas** y desmarque la opción **Callhome**.
     3. Pulse **Aceptar**.
     {: note}
