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

# Création de clés et génération de la demande de signature de certificat (CSR)
{: #create-keys-and-generate-the-certificate-signing-request-csr-}

Dans cette sous-section, nous allons créer une paire de clés qui sera utilisée pour générer une demande de signature de certificat (CSR), puis commander/demander un certificat par son intermédiaire.

1.	Tout d'abord, validez la liste d'objets dans VPX. Utilisez le mot de passe spécifié pour cette partition lors du processus de création.

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	```

	Cette sortie confirme l'absence d'objets, car le résultat est vide.

	Vérifiez ensuite que le nombre d'objet est 0 dans HSM en affichant les détails de la partition :

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

	La commande ci-dessus utilise la syntaxe suivante :

	```
	partition show -p <partition_name>
	```

2.	A l'aide de l'utilitaire de gestion des certificats (CMU) de VPX, créez une paire de clés avec la commande ci-dessous. Là encore, utilisez le mot de passe approprié pour la partition.

	```
	root@IBMADC690867-s6dr# cmu gen -modulusBits=2048 -publicExponent=65537 -sign=T -verify=T -label=NSkey_s6dr
	Please enter password for token in slot 0 : **********

	Select RSA Mechanism Type - 
	[1] PKCS [2] FIPS 186-3 Only Primes [3] FIPS 186-3 Auxiliary Primes : 1
	```

	Dans la syntaxe ci-dessus, le paramètre `modulusBits` indique la longueur (exprimée en bits) des clés RSA, tandis que `publicExponent` définit l'exposant public à utiliser pour la génération des clés (dont la valeur doit être 3, 17 ou 65537). Le mot clé “label” permet de spécifier une balise facilitant son référencement et son identification ultérieures. Pour en savoir plus sur les deux autres paramètres supplémentaires, reportez-vous au document [Utilities Reference Guide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/utilities_reference_guide.pdf){: new_window} (en anglais).

3.	Vérifiez que les objets ont été créés. Dans VPX :

	```
	root@IBMADC690867-s6dr# cmu list
	Please enter password for token in slot 0 : **********
	handle=76       label=NSkey_s6dr
	handle=73       label=NSkey_s6dr
	```

	Dans HSM :

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

4.	A l'aide des clés créées à l'étape précédente, générez une demande CRS par le biais de l'utilitaire CMU.

	Assurez-vous d'utiliser les valeurs correctes/appropriées pour le nom commun (CN) et l'e-mail (E). Le paramètre CN doit correspondre au nom de domaine complet qui sera utilisé dans l'enregistrement DNS A associé au VPX, tandis que le paramètre E sera utilisé pour envoyer les détails d'approvisionnement du certificat une fois celui-ci demandé/commandé.

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

	Dans la sortie ci-dessus, le nom de fichier peut être n'importe quel fichier ayant une extension .csr. Toutefois, nous vous conseillons de lui attribuer un nom suffisamment explicite.

5.	Vérifiez que le fichier a été créé.

	```
	root@IBMADC690867-s6dr# ls
	certreqnss6dr.csr       common                  multitoken              	server.pem
	ckdemo                  configurator            openssl.cnf             	uninstall.sh
	cmu                     lunacm                  salogin                 vtl
	```
