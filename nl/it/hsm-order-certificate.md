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

# Ordinazione di un certificato SSL
{: #order-an-ssl-certificate}

SSL (Secure Sockets Layer) è una tecnologia che crittografa il traffico tra l'applicazione client e quella server e viene eseguita utilizzando un sistema di chiave pubblica/chiave privata che utilizza un certificato SSL.

I certificati SSL contengono la chiave pubblica del server, le date per le quali il certificato è valido, un nome host per cui il certificato è valido e una firma dell'autorità di certificazione (CA, certificate authority) che lo emesso.

IBM© Cloud offre certificati che possono essere acquisiti e acquistati senza dover ricorrere a fornitori/siti di terze parti. 

IBM Cloud offre certificati SSL annuali e biennali per i clienti che offrono diversi benefici, inclusi:

* Autenticazione completa per la verifica dell'identità aziendale e della proprietà del dominio
* Crittografia da 40 a 256 bit su tutte le transazioni online
* Scansione malware giornaliera del sito web per garantire la protezione del tuo sito e dei tuoi clienti

Se stai eseguendo più domini, puoi acquistare un certificato SSL per ciascun dominio.

Per ulteriori informazioni sui certificati SSL, fai riferimento ai seguenti articoli IBM Cloud:

* [Informazioni sui certificati SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-about-ssl-certificates)
* [Introduzione alla tecnologia SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-introduction-to-ssl-technology)
* [Pianificazione di SSL](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-planning-for-ssl)


Per ordinare un certificato SSL da utilizzare con il tuo Citrix Netscaler VPX, esegui la seguente procedura:

1.	Nella CLI shell VPX, visualizza il testo CSR aprendo il file CSR creato in precedenza nel passo [Creazione di chiavi e generazione di CSR (Certificate Signing Request)](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-create-keys-and-generate-the-certificate-signing-request-csr-):

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

2.	Copia il contenuto del file a partire da `---BEGIN NEW CERTIFICATE REQUEST---` fino a `---END NEW CERTIFICATE REQUEST---`.

3.	Segui [queste istruzioni](/docs/infrastructure/ssl-certificates?topic=ssl-certificates-getting-started-tutorial#ordering-ssl-certificates) per inserire l'ordine, incollando il testo del tuo file CSR nel campo appropriato. Nel seguente esempio, è stato scelto `RapidSSL 1 Year`.

	<img src="images/5-Order-Certificate_1.png" alt="immagine" style="width: 550px;"/>

	Come mostrato, il sistema elabora e interpreta il testo CSR, quindi visualizza il risultato nella pagina seguente.

	Assicurati di selezionare un account email e un dominio/dominio secondario validi in quanto tale operazione costituisce il metodo designato per convalidare la proprietà del dominio.

	Conferma i dettagli del tuo ordine e fai clic su **Place Order**.

4. Riceverai una conferma dell'ordine con i dettagli della richiesta di certificato all'account che hai indicato.

	Fai clic sul link fornito nell'email per approvare la richiesta di convalida del dominio. A questo punto, la richiesta SSL dovrebbe essere pronta per iniziare a svolgere l'attività. 
