---

copyright:
  years: 2018
lastupdated: "2018-11-12"

keywords: hsm, security, certificate, order

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

# Solicitar un certificado SSL
{: #order-an-ssl-certificate}

La capa de sockets seguros (SSL) es una tecnología que cifra el tráfico entre la aplicación cliente y la aplicación de servidor y que se consigue mediante un sistema de clave pública/privada que utiliza un certificado SSL.

Los certificados SSL contiene la clave pública del servidor, fechas en las que el certificado es válido, un nombre de host en el que el certificado es válido y una firma de la autoridad de certificado que lo ha emitido.

IBM© Cloud ofrece certificados que se pueden adquirir sin tener que pasar por un sitio/proveedor de terceros.

IBM Cloud ofrece certificados SSL anuales y bianuales para clientes que ofrecen diversos beneficios, entre ellos:

* Autenticación completa para la identidad empresarial y la verificación de propiedad del dominio
* Cifrado de 40 a 256 bits en todas las transacciones en línea
* Escaneo diario de malware en el sitio web para garantizar que tanto el sitio como los clientes están protegidos

Si está ejecutando varios dominios, puede adquirir un certificado SSL para cada dominio.

Para obtener más información sobre los certificados SSL, consulte los siguientes artículos de IBM Cloud:

* [Acerca de los certificados SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [Introducción a la tecnología SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [Planificación para SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)

Para solicitar un certificado SSL y utilizarlo con {{site.data.keyword.vpx_full}}, realice el procedimiento siguiente:

1.	En la CLI de shell de VPX, visualice el texto CSR abriendo el archivo CSR creado anteriormente en el paso [Crear claves y generar la solicitud de firma de certificado (CSR)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-):

	```
	root@IBMADC690867-s6dr# cat certreqnss6dr.csr
	-----BEGIN NEW CERTIFICATE REQUEST-----
	MIIC5jCCAc4CAQAwgaAxCzAJBgNVBAYTMRcwFQYDVQQIEw5Ob3J0aCBDYXJv
	bGluYTEPMA0GA1UEBxMGRHVyaGFtMQwwCgYDVQQKEwNJQk0xDDAKBgNVBAsTA0hT
	TTEoMCYGA1UEAxMfaHNW50Ny5wcm9qZWN0Z29sZGZpbmNoLm5ldDEhMB8G
	CSqGSIb3DQEJARYSanBtb25nZUBjci5pYm0uY29tMIIBIjANBgkqhkiG9w0BAQEF
	/pXQN+a55HhWmnyj5gThAprOoN8DeiVN+1HI+PA+g1
	r4+8dKA1xz+jPhWDQgQYb3Wnh8VK8Ouids6uFnsoc3KDymbzoWZYctp8PA6uBzJ/
	25RGiZquRu9MYJIWkQ46WQ14PoJ8BiYuJa/N6L47+Jr2vaCntmXBU4rFrjctHqq8
	Hct9q5OVYXbYLQB+MM3gYyyFBQpZ1sHZD4D6K3AISRGsOE9rrovGjUfO8mLKE6a
	AQEFBQADggEBAMe+kmdPNtt8LOpaAy+u5i9GpgHfH5zW2sX4Lj7srkqwmyxavqjE
	XvM9PPudXV9OCUWewtlm/Eqo1pYIRudFBrjg5UJyKpM4sWWdKIrTk8RZusdOUvKU
	0vBRJRJ3Yy/1olXFO05FFSotAyB9P5v9siMwdWUhM9pSiGwoNXCB74m2sxgUh10J
	H0IvDl3SL4ptosV10KJtbOiO/YV9XXNaW8/X/2uM9Y3stcnSvzJGrFlPmbhK7Vsd
	uL6/wSnV1E70CDT+KPPapzVJr/S8nP5xHVVl/5/JUGZa8rx01g9EBmX36H3T
	kHD85XOkSI4y04Y3t6pMVbIAz0vipOmHYlM=
	-----END NEW CERTIFICATE REQUEST-----
	```

2.	Copie el contenido del archivo empezando por `---BEGIN NEW CERTIFICATE REQUEST---` hasta `---END NEW CERTIFICATE REQUEST---`.

3.	Siga [las instrucciones](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates) para realizar el pedido, pegando el texto del archivo CSR en el campo adecuado. En el ejemplo siguiente se ha elegido `RapidSSL 1 Year`.

	<img src="images/5-Order-Certificate_1.png" alt="dibujo" style="width: 550px;"/>

	Tal como se muestra, el sistema procesa e interpreta el texto CSR y los muestra en la página siguiente.

	Asegúrese de seleccionar una cuenta de correo electrónico válida y un dominio/subdominio, ya que este es el método designado para validar la propiedad del dominio.

	Confirme los detalles del pedido y haga clic en **Realizar pedido**.

4. Recibirá una confirmación de pedido con los detalles de la solicitud de certificado en la cuenta que ha indicado.

	Pulse el enlace entre comillas del correo electrónico para aprobar la solicitud de validación de dominio. En este punto, la solicitud de SSL debe estar lista para empezar el cumplimiento.
