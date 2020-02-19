---

copyright:
  years: 2018
lastupdated: "2019-11-12"

keywords: hsm, security, keys, csr

subcollection: citrix-netscaler-vpx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank_"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Create keys and generate the Certificate Signing Request (CSR)
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

You can create a key pair to generate a Certificate Signing Request (CSR). In addition, you'll need the key pair to order or request a certificate to further configure the HSM for the {{site.data.keyword.vpx_full}}.

1.	First, confirm the object list in VPX. Use the specified password for this partition during creation.

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : 	**********
	```

	This output confirms no objects exist as the output is blank/empty.

	Then verify the object count is 0 in the HSM by displaying the partition details:

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

	The command listed above uses the below syntax:

	```
	partition show -p <partition_name>
	```

2.	Using the Certificate Management Utility (CMU) in VPX, create a key pair using the command shown below. Once again, use the designated partition password.

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	Select RSA Mechanism Type -
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	In the above syntax, the `modulusBits` parameter indicates the length in bits of the RSA keys, while `publicExponent` defines the public exponent value to be used for the generation of the keys, this must be set to 3, 17 or 65537. The “label” keyword is used to specify a tag for it to be easily referenced and identified later. For more information about the other two / additional parameters check the [Utilities Reference Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window}.

3.	Confirm objects were created. In VPX:

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	In the HSM:

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

4.	Using the keys created in the previous step, generate a CSR using the CMU utility.

	Make sure to use the correct/appropriate values for Common Name (CN) and E-mail (E), the first one should match the FQDN that will be used in the DNS A record associated with the Virtual Server/IP (VPX). The E parameter will be used to send certificate procurement details after this is requested/ordered.

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

	In the output listed above, the filename can be anything with a .csr extension, however, a meaningful description is recommended.

5.	Confirm creation of the file

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
