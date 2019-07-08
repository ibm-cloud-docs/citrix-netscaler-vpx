---



copyright:
  years: 2017
lastupdated: "2018-11-12"

keywords: cache, configure, configuration, http, traffic

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

# Configurar la redirección de memoria caché para el tráfico HTTP(S)
{: #configure-cache-redirection-for-http-traffic}

Para configurar la redirección de la memoria caché para el tráfico HTTP o HTTPS, siga estos pasos:

1. Vaya a **Gestión de tráfico > Redirección de memoria caché > Servidores virtuales** y pulse **Añadir**.
2. Especifique el nombre del servidor virtual proxy directo. Seleccione el protocolo **HTTP** y el tipo de memoria caché **Reenvío** de sus respectivas listas desplegables. A continuación, asigne una dirección IP a este servidor virtual desde la subred privada.

	<img src="images/fp12.png" alt="dibujo" style="width: 300px;"/>

	Pulse **Aceptar** para continuar.

3. Revise la página de resumen y pulse **Aceptar**.  
4. Pulse **Configuración de tráfico** para ver los valores de configuración adicionales.
5. Desde Valores de tráfico, seleccione una de las tres opciones de redirección siguientes, en función de los requisitos:
	* **Memoria caché** - Direcciona todas las solicitudes de salida a la agrupación de servidor de memoria caché local.
	* **Política** - Comprueba la política de redirección de memoria caché para determinar si la solicitud se debe reenviar a la agrupación de servidor de memoria caché o a los servidores de destino (origen).
	* **Origen** – Direcciona todas las solicitudes de salida a los servidores (origen) de destino respectivos.

6. En la lista desplegable **Nombre de servidor virtual DNS**, seleccione el servidor virtual DNS configurado anteriormente y la opción **Redirigir** a **Origen**.

	<img src="images/fp13.png" alt="dibujo" style="width: 300px;"/>

	**NOTA:** El valor **Servidor virtual de destino** se utiliza cuando el tráfico de salida se va a dirigir a la agrupación de servidores de memoria caché local. Déjelo en blanco cuando desee dirigir todo el tráfico de salida a los servidores de origen.

7. Pulse **Aceptar** seguido de **Terminado**.
