---

copyright:
  years: 2024
lastupdated: "2024-08-02"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Create keys and generate the Certificate Signing Request (CSR)
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

You can create a key pair to generate a Certificate Signing Request (CSR). In addition, you need the key pair to order or request a certificate to further configure the HSM for the {{site.data.keyword.vpx_full}}.

1. First, confirm the object list in VPX. Use the specified password for this partition during creation.

   ```sh
   root@IBMADC690867-s6dr# cmu list
   Please enter password for token in slot 0 : 	**********
   ```
   
   This output confirms that no objects exist as the output is empty.
   
   Then verify that the object count is `0` in the HSM by displaying the partition details:
   
   ```sh
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
   
   The command that is listed in the previous example uses the following syntax:
   
   ```sh
   partition show -p <partition_name>
   ```
   
2. Using the Certificate Management Utility (CMU) in VPX, create a key pair by using the command that is shown in the following example. Once again, use the designated partition password.

   ```sh
   root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
   Please enter password for token in slot 0 : **********
   
   Select RSA Mechanism Type -
   [1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
   ```
   
   In the previous syntax, the `modulusBits` parameter indicates the length in bits of the RSA keys, while `publicExponent` defines the public exponent value to be used for the generation of the keys. `publicExponent` must be set to `3`, `17`, or `65537`. The “label” keyword is used to specify a tag for it to be easily referenced and identified later. For more information about, the other two / extra parameters check the [Utilities Reference Guide](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: external}.

3. Confirm that objects were created. In VPX:
   
   ```sh
   root@IBMADC690867-s6dr# cmu list
   Please enter password for token in slot 0 : **********
   handle=76       label=NSkey_s6dr
   handle=73       label=NSkey_s6dr
   ```
   
   In the HSM:
   
   ```sh
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
   
4. With the keys created in the previous step, generate a CSR with the CMU utility.
   
   Make sure to use the appropriate values for Common Name (CN) and E-mail (E). The first matches the FQDN used in the DNS A record that is associated with the Virtual IP (VPX). The E parameter will be used to send certificate procurement details after the request.

   ```sh
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
   
   However, in the output that is listed, the filename can be anything with a .csr extension a meaningful description is recommended.
   
5. Confirm creation of the file.
   
   ```sh
   root@IBMADC690867-s6dr# ls
   certreqnss6dr.csr       common                  multitoken              	server.pem
   ckdemo                  configurator            openssl.cnf             	uninstall.sh
   cmu                     lunacm                  salogin                 vtl
   ```
