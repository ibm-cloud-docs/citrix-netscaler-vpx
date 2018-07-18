---
copyright:
  years: 1994, 2018

lastupdated: "2018-06-28"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurar Citrix Netscaler VPX para alta disponibilidad (HA)

Los equilibradores de carga se utilizan para equilibrar el tráfico en varios servidores de aplicaciones para mejorar el rendimiento y la estabilidad en una aplicación escalable. Sin embargo, un solo equilibrador de carga es un único punto de anomalía. Evite esto configurando un par de alta disponibilidad (HA) de Netscaler VPX. La configuración de un par de alta disponibilidad requiere dos servidores Netscaler VPX. El servidor secundario entra para continuar el equilibrio de carga si falla el primario. 

La SNIP (subred IP) es la IP vista por los servidores de equilibrio de carga como IP de origen de las solicitudes (conexiones) realizadas a la VIP (IP virtual) del Netscaler VPX. Normalmente, en una configuración de par de HA, la SNIP no cambia, pero es posible que suceda durante un suceso de migración tras error. Cuando los dos Netscalers están en la misma subred, es posible que la SNIP del secundario cambie la SNIP utilizada originalmente por el primario. Esto no causará ninguna confusión a los servidores que manejan la solicitud.

Para una configuración de alta disponibilidad, ambos NetScalers deben estar en la misma VLAN y en la misma subred.

Antes de empezar la configuración de alta disponibilidad, asegúrese de realizar las siguientes acciones de requisito previo:

1. Si el par estará configurado como activo-activo, cualquier subred de VIP añadida a las instancias debe ser del tipo "Direccionado a VLAN".
* Si el par estará configurado como activo-pasivo, cualquier subred de VIP añadida a las instancias debe ser del tipo "Direccionado a VLAN" o "Secundario direccionado a IP" y redireccionarse a la dirección IP pública del nodo primario.

Después de pedir los dos servidores de Netscaler VPX en la VLAN necesaria y pedir las subredes VIP y SNIP para cumplir los requisitos previos para la configuración del par de alta disponibilidad, puede continuar con lo siguiente:

1. Abra dos ventanas de navegador e inicie sesión en la interfaz avanzada en ambos NetScalers. En el NetScaler secundario, vaya a **Sistema > Administración de usuarios > Usuarios** y establezca la contraseña raíz en la misma que el NetScaler primario. A continuación, actualice la contraseña en el archivo en el portal de {{site.data.keyword.BluSoftlayer_notm}} en la página de detalles del dispositivo para que coincida con la contraseña establecida para el secundario.

2. En el VPX que desea que sea el secundario, pulse **Sistema > Alta disponibilidad**, pulse con el botón derecho en la primera línea y pulse **Editar**. Seleccione **Permanecer secundario** en el recuadro desplegable de configuración de Estado de alta disponibilidad y pulse **Aceptar**.

3. Seleccione **Añadir**. Especifique la dirección IP del sistema de otros VPX (se encuentran en el separador de alta disponibilidad en el primario) y especifique los detalles del inicio de sesión como root en la parte inferior. Deje el recuadro **Activar INC** sin marcar. Pulse **Aceptar**. 
	
	Si sucede un erro diciendo que las IP no están en la misma subred, es posible que ambos servidores VPX no estén en la misma VLAN. De lo contrario, ahora debería poder abrir el servidor primario y seleccionar el botón **Actualizar** para ver los servidores que operan en alta disponibilidad. 

	La IP de gestión del nuevo NetScaler para el secundario será una dirección IP inferior al anterior. Si no puede obtener acceso al VPX secundario, elimine la alta disponibilidad desde la línea de mandatos utilizando:

	`sh ha node`

	Elimine el nodo de HA:
	
	`rm ha node 1`

4. En el VPX primario debería ver que el VPX remoto se está sincronizando. Vaya al servidor secundario y compruebe la configuración de **Red > IP**. Debería ver la VIP del servidor primario y otras IP listadas como pasivas.

6. Vuelva a **Sistema > Alta disponibilidad** en el servidor secundario y pulse **Editar**. Seleccione **HABILITADO** en el recuadro desplegable y pulse **Aceptar**.

7. Fuerce una migración tras error de prueba. Actualice la pantalla y observe las direcciones IP que pasan a estar en activo en el secundario. Realice de nuevo una migración tras error y vea como pasan a estar en pasivo. Haga ping en las IP para asegurar que funcionan.

8. El servidor primario debe estar ahora etiquetado como primario y el secundario debe informar de que tiene un estado de sincronización de éxito.
