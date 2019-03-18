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

# Crear claves y generar la Solicitud de firma de certificado (CSR)
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

En esta subsección crearemos un par de claves que se utilizará para generar una Solicitud de firma de certificado (CSR) y para pedir/solicitar un certificado con la misma.

1.	Primero, confirme la lista de objetos en VPX. Utilice la contraseña especificada para esta partición durante la creación.

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	```

	Esta salida confirma que no existe ningún objeto ya que la salida está en blanco/vacía.

	A continuación, verifique que el recuento de objetos es 0 en HSM visualizado los detalles de partición:

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	Partition Name:                            partition6
	Partition SN:                              534071053
	Partition Label:                           partition6
	Partition Owner Locked Out:                no
	Partition Owner PIN To Be Changed:         no
	Partition Owner Login Attempts Left:       10 before Partition Owner is Locked Out
	Legacy Domain Has Been Set:                no
	Partition Storage Information (Bytes):     Total=207559, Used=0, Free=207559
	Partition Object Count:                    0

	Command Result : 0 (Success)
	```

	El mandato que aparece en la lista anterior utiliza la sintaxis siguiente:

	```
	partition show -p <nombre_partición>
	```

2.	Cuando utilice el programa de utilidad de gestión de certificado (CMU) en VPX, cree un par de claves utilizando el mandato que se muestra a continuación. Una vez más, utilice la contraseña de partición designada.

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	Select RSA Mechanism Type - 
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	En la sintaxis anterior, el parámetro `modulusBits` indica la longitud en bits de las claves RSA, mientras que `publicExponent` define el valor de exponente público que se va a utilizar para la generación de claves; debe establecerse en 3, 17 o 65537. La palabra clave "etiqueta" se utiliza para especificar la etiqueta para que se haga referencia a ella de manera sencilla y se pueda identificar más adelante. Para obtener más información sobre otros dos parámetros adicionales, consulte la [Guía de referencia de programas de utilidad ![Icono de enlace externo](../../icons/launch-glyph.svg "Iono de enlace externo")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Confirme los objetos que se han creado. En VPX:

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	En HSM:

	```
	[jpmongehsm2] lunash:>partition show -p partition6

	Partition Name:                            partition6
	Partition SN:                              534071053
	Partition Label:                           partition6
	Partition Owner Locked Out:                no
	Partition Owner PIN To Be Changed:         no
	Partition Owner Login Attempts Left:       10 before Partition Owner is Locked Out
	Legacy Domain Has Been Set:                no
	Partition Storage Information (Bytes):     Total=207559, Used=1660,  Free=205899
	Partition Object Count:                    2

	Command Result : 0 (Success)
	```

4.	Utilizando las claves creadas en el paso anterior, genere el CSR utilizando el programa de utilizada de CMU.

	Asegúrese de utilizar los valores correctos/adecuados para Nombre común (CN) y Dirección de correo electrónico (E); el primero debe coincidir con el FQDN que se utilizará en el DNS, un registro asociado con el servidor virtual/IP (VPX). El parámetro E se utilizará para enviar los detalles de aprovisionamiento de certificados después de que se solicite.

	```
	root@IBMADC690867-s6dr# cmu requestcertificate

	Please enter password for token in slot 0 : **********

	Enter Subject 2-letter Country Code (C) : US
	Enter Subject State or Province Name (S) : North Carolina
	Enter Subject Locality Name (L) : Durham
	Enter Subject Organization Name (O) : IBM
	Enter Subject Organization Unit Name (OU) : HSM
	Enter Subject Common Name (CN) : hsmclient7.projectgoldfinch.net   
	Enter EMAIL Address (E) : user@yourdomain.com
	Enter output filename : certreqnss6dr.csr
	```

	En la salida de la lista anterior, el nombre de archivo puede ser cualquiera con una extensión .csr; sin embargo, se recomienda una descripción significativa.

5.	Confirme la creación del archivo

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
