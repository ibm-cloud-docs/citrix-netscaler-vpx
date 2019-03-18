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

# Inicializar IBM Hardware Security Module (HSM)
{: #initialize-ibm-hardware-security-module-hsm-}

La mayoría de las configuraciones requieren la inicialización del dispositivo HSM. Sin esto, solo se pueden ejecutar determinados mandatos `show`.

Para inicializar el dispositivo, siga los pasos siguientes:

1.	Conéctese mediante SSH en el dispositivo IBM© Hardware Security Module con las credenciales listadas en el portal de control en **Dispositivos > Lista de dispositivo > Expandir nombre de HSM**.

	De forma alternativa, puede utilizar la autenticación de clave pública. Para obtener más información, revise [Guía de administración de dispositivo (página 38)![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){:new_window}.

	**NOTA:** Por lo general, el acceso SSH está habilitado y permitido de forma predeterminada. Si tiene problemas al conectarse con el SSH, compruebe la seguridad y direccionamiento de la infraestructura.

2. Ejecute el mandato `hsm init`:

	```
	[jpmongehsm2] lunash:>hsm init -l jpmonge

	Please enter a password for the HSM Administrator:
	> ********

	Please re-enter password to confirm:
	> ********

	Please enter a cloning domain to use for initializing this HSM:
	> ********

	Please re-enter cloning domain to confirm:
	> ********

	CAUTION:  Are you sure you wish to initialize this HSM?

	Type 'proceed' to initialize the HSM, or 'quit'
		to quit now.
		> proceed
		'hsm init' successful.

	Command Result : 0 (Success)
  	```

	Donde la sintaxis utilizada es: `hsm init -l <hsmlabel>`

El parámetro o etiqueta `-l` es un parámetro utilizado para asignar un identificador al HSM y puede ser cualquier texto o descripción significativa relacionados con los negocios, el administrador o el rol que cumple. La contraseña del administrador de HSM será la contraseña designada para el responsable de seguridad de HSM y es un perfil necesario para crear y configurar objetos criptográficos, así como realizar cambios en el entorno de HSM.

Por último, el dominio de clonación es un identificador compartido que permite que los objetos se forme entre un grupo de HSM. Esto se suele utilizar para la copia de seguridad y/o la alta disponibilidad (HA).

Consulte la [Guía de referencia de los mandatos LunaSH ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: new_window} para ver todos los mandatos disponibles soportados en la CLI de HSM.
