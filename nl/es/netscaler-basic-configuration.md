---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuración básica del equilibrio de carga
Considere una empresa que tiene un sitio web de comunidad social básico donde los usuarios pueden registrarse en una cuenta que no requiere información confidencial, después el usuario puede iniciar sesión y publicar fotos de sus mascotas. Hay tres servidores de aplicaciones/web y servidor de base de datos para realizar copia de seguridad. El dominio y DNS están alojados con {{site.data.keyword.BluSoftlayer_notm}}, y puesto que tienen un entorno pequeño, los servidores de web/aplicación y NetScaler están todos en la misma VLAN. Esto simplifica las cosas, ya que no se necesita ninguna configuración adicional para NetScaler para establecer una política de equilibrio de carga básica. El procedimiento siguiente es una explicación simplista del flujo de tráfico en esta instancia:

1. Un usuario introduce el URL en su navegador.
2. El registro de DNS del URL apunta a una de las VIP públicas en NetScaler.
3. El NetScaler recibe el tráfico en ese VIP y toma nota del protocolo de tráfico que se utiliza (tráfico del puerto HTTP 80).
4. El NetScaler pasa entonces el tráfico a uno de los servidores en la agrupación de servidores, basándose en el método de equilibrio definido (round robin, IP de persistencia, etc.).
5. El servidor acepta el tráfico y el usuario se conecta y registra.

Para lograrlo, el NetScaler debe configurarse para manejar este tráfico. Como la VIP, la IP del servidor de DNS y la SNIP ya están configuradas, esto simplifica la configuración. 

En la GUI de NetScaler, en la pantalla de configuración, expanda la **Gestión de tráfico** en el lado izquierdo. Expanda la subsección titulada **Equilibrio de carga**. Luego diga a NetScaler que servidores de destino se incluirán en la política de equilibrio de carga, siguiendo este procedimiento:

1. En Equilibrio de carga, pulse **Servidores**.
2. Pulse **Añadir**.
3. Especifique el nombre de servidor del servidor (por ejemplo, Web1).
4. Especifique la dirección IP del servidor.
5. Deje el campo **Dominio de tráfico** en blanco, ya que solo nos interesa utilizar el dominio predeterminado en este caso de ejemplo.
6. Escriba cualquier comentario que desee sobre este servidor.
7. Pulse **Crear**.

Repita este procedimiento para todos los servidores en la agrupación.  

**Sugerencia:** Para mantener los servidores fácilmente identificables, utilice una convención de nomenclatura similar para los servidores dentro de la misma agrupación (por ejemplo, Web1, Web2, Web3, etc.).

A continuación, cree sus servicios. Podrá crear un servicio para cada servidor que acabe de especificar. El servicio es lo que configura la conexión entre el NetScaler y los servidores de la agrupación. Cada servicio tiene un nombre y especifica una dirección IP, un puerto y el tipo de datos que se sirve.

1. Pulse **Gestión de tráfico > Equilibrio de carga > Servicios**.
2. Pulse **Añadir**.
3. Cree un servicio para cada servidor creado anteriormente, utilizando la misma información.

A continuación, cree un servidor virtual. El servidor virtual es una especie de conexión virtual entre la VIP utilizada para los servidores y servicios de equilibro de carga creados anteriormente.

1. Pulse **Gestión de tráfico > Equilibrio de carga > Servidores virtuales**.
2. Pulse **Añadir**.
3. Ponga nombre al servidor virtual.
4. Designe el protocolo que va a equilibrar (HTTP).
5. Deje el tipo de dirección IP con el valor predeterminado (direcciones IP). El campo de dirección IP es donde especificará la VIP que utilizará como punto de entrada para todos los usuarios.
6. Designe el puerto. El puerto predeterminado es el 80.
7. Pulse **Aceptar**.

Ahora, enlace los servicios que ha creado con su servidor virtual.

1. En la pantalla Servidores virtuales, pulse el enlace **Sin enlace de servicio de servidor virtual de equilibrio de carga**.
2. Enlace cada uno de los servicios creados anteriormente con el servidor virtual.
3. Pulse **Listo**.
4. Pulse el botón **Renovar**. El Estado y el Estado eficaz se mostrarán en verde.

Ha creado una agrupación de equilibrio de carga y una política para su sitio web.
