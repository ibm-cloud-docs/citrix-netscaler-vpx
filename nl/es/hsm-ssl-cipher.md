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

# Crear y aplicar una nueva suite de cifrado
{: #create-and-apply-a-new-cipher-suite}

Una suite de cifrado es una combinación de autenticación, cifrado, código de autenticación de mensajes (MAC) y algoritmos de intercambio de claves que se utilizan para negociar la configuración de seguridad para los protocolos SSL y TLS.

Para garantizar una autenticación adecuada, debe asegurarse de que Citrix Netscaler VPX utiliza la mejor combinación de cifrados.

Para obtener más información sobre las suites de cifrado de SSL y otras prácticas recomendadas, visite los enlaces siguientes:

* [Conseguir una puntuación sobresaliente en SSLlabs.com con Citrix NetScaler ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.citrix.com/blogs/2018/05/16/scoring-an-a-at-ssllabs-com-with-citrix-netscaler-q2-2018-update/){:new_window} – actualización del segundo trimestre de 2018 (consulte los pasos tres y cinco en la guía de mandatos)
* [Prácticas recomendadas del despliegue SSL y TLS ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices#23-use-secure-cipher-suites){:new_window}
* [¿Cómo puedo configurar ECC en NetScaler? ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://support.citrix.com/article/CTX205289){:new_window}

**NOTA:** Este tema se centra en configuraciones específicas y necesarias para los cifrados SSL. La información de los enlaces anteriores puede proporcionar valores adicionales que se pueden aplicar para optimizar la operación SSL.

Para crear una nueva suite de cifrado que dé prioridad a los cifrados AEAD, ECDHE y ECDSA, realice el procedimiento siguiente:

1.	Especifique los mandatos siguientes simultáneamente en la CLI de Citrix VPX y asegúrese de que se aplican todos:

	```
	add ssl cipher SSLLABS
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-ECDSA-AES256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-ECDSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-128-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-ECDHE-RSA-AES-256-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES128-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-ECDHE-RSA-AES256-SHA
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES128-GCM-SHA256
	bind ssl cipher SSLLABS -cipherName TLS1.2-DHE-RSA-AES256-GCM-SHA384
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-DHE-RSA-AES-256-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-128-CBC-SHA
	bind ssl cipher SSLLABS -cipherName TLS1-AES-256-CBC-SHA
	```

	La sintaxis de los mandatos anteriores es la siguiente:

	```
	add ssl cipher <cipherGroupName>
	bind ssl cipher <cipherGroupName> -cipherName <string>
	```

2.	Confirme que el cifrado se ha añadido a Citrix Netscaler VPX:

	```
	> show ssl cipher SSLLABS
	1)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES128-GCM-SHA256       Priority : 1
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02b
	2)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES256-GCM-SHA384       Priority : 2
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc02c
	3)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES128-SHA256   Priority : 3
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA-256   HexCode=0xc023
	4)      Cipher Name: TLS1.2-ECDHE-ECDSA-AES256-SHA384   Priority : 4
	        Description: TLSv1.2 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA-384   HexCode=0xc024
	5)      Cipher Name: TLS1-ECDHE-ECDSA-AES128-SHA        Priority : 5
	        Description: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(128)  Mac=SHA1   HexCode=0xc009
	6)      Cipher Name: TLS1-ECDHE-ECDSA-AES256-SHA        Priority : 6
	        Description: SSLv3 Kx=ECC-DHE  Au=ECDSA Enc=AES(256)  Mac=SHA1   HexCode=0xc00a
	7)      Cipher Name: TLS1.2-ECDHE-RSA-AES128-GCM-SHA256 Priority : 7
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0xc02f
	8)      Cipher Name: TLS1.2-ECDHE-RSA-AES256-GCM-SHA384 Priority : 8
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0xc030
	9)      Cipher Name: TLS1.2-ECDHE-RSA-AES-128-SHA256    Priority : 9
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA-256   HexCode=0xc027
	10)     Cipher Name: TLS1.2-ECDHE-RSA-AES-256-SHA384    Priority : 10
	        Description: TLSv1.2 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA-384   HexCode=0xc028
	11)     Cipher Name: TLS1-ECDHE-RSA-AES128-SHA  Priority : 11
	        Description: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0xc013
	12)     Cipher Name: TLS1-ECDHE-RSA-AES256-SHA  Priority : 12
	        Description: SSLv3 Kx=ECC-DHE  Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0xc014
	13)     Cipher Name: TLS1.2-DHE-RSA-AES128-GCM-SHA256   Priority : 13
	        Description: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(128) Mac=AEAD   HexCode=0x009e
	14)     Cipher Name: TLS1.2-DHE-RSA-AES256-GCM-SHA384   Priority : 14
	        Description: TLSv1.2 Kx=DH       Au=RSA  Enc=AES-GCM(256) Mac=AEAD   HexCode=0x009f
	15)     Cipher Name: TLS1-DHE-RSA-AES-128-CBC-SHA       Priority : 15
	        Description: SSLv3 Kx=DH       Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x0033
	16)     Cipher Name: TLS1-DHE-RSA-AES-256-CBC-SHA       Priority : 16
	        Description: SSLv3 Kx=DH       Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0039
	17)     Cipher Name: TLS1-AES-128-CBC-SHA       Priority : 17
	        Description: SSLv3 Kx=RSA      Au=RSA  Enc=AES(128)  Mac=SHA1   HexCode=0x002f
	18)     Cipher Name: TLS1-AES-256-CBC-SHA       Priority : 18
	        Description: SSLv3 Kx=RSA      Au=RSA  Enc=AES(256)  Mac=SHA1   HexCode=0x0035
 	Done
 	```

3.	Elimine el enlace de la suite de cifrado predeterminada del servidor virtual y enlace el grupo personalizado creado en el paso anterior:

	```
	unbind ssl vserver https_vip2 -cipherName DEFAULT

	bind ssl vserver https_vip2 -cipherName SSLLABS

	bind ssl vserver https_vip2 -eccCurveName ALL
	```

	The syntax for the previous commands is:

	```
	unbind ssl cipher <cipherGroupName> -cipherName <string>
	bind ssl vserver <vServerName> -cipherName <string>
	bind ssl vserver <vServerName> -eccCurveName <eccCurveName>
	```

4.	Confirme los cambios en el servidor virtual:

	```
	> show ssl vserver https_vip2

	[OUTPUT OMITTED]
		ECC Curve: P_256, P_384, P_224, P_521

	1)      CertKey Name: hsmclient7ns      Server Certificate

	1)      Cipher Name: SSLLABS
		Description: User Created Cipher Group
 	Done
	```

5.	(OPCIONAL) La redirección HTTP se puede habilitar para redirigir a los usuarios a un sitio web seguro cuando crean una solicitud HTTP (en contraposición a HTTPS).

	Consulte [Cómo configurar HTTP en la redirección HTTPS en NetScaler ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://support.citrix.com/article/CTX201201){:new_window} para obtener instrucciones de configuración.

6.	Pruebe la conexión HTTPS abriendo un navegador web y especificando el nombre de dominio completo. El sitio debe cargar el contenido representado por el servicio HTTP detrás de Citrix VPX.

	También puede visualizar los detalles del certificado pulsando en el icono de candado junto al URL en el navegador para visualizar la información del certificado.

	<img src="images/21-check-certificate.png" alt="drawing" style="width: 350px;"/>

	Si la redirección se ha configurado en el paso cinco, el sitio seguro también se cargará cuando se utilice una solicitud HTTP.
