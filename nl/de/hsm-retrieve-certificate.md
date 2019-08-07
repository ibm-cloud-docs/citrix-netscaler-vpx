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

# Zertifikat abrufen und übertragen
{: #retrieve-and-transfer-the-certificate}

Rufen Sie das zuvor bestellte SSL-Zertifikat ab, so dass Sie für seine Installation und Konfiguration in der nächsten Anleitung, [SSL-Auslagerung mit {{site.data.keyword.vpx_full}} konfigurieren und optimieren](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-configuring-and-tuning-ssl-offload-with-citrix-netscaler-vpx), bereit sind.

1. Kurz nach der Validierung des Eigentumsrechts der Domäne sollten Sie eine E-Mail erhalten, in der der Abschluss der Zertifikatserfüllung und das Zertifikat selbst bestätigt werden.

	Kopieren Sie den Text von `---BEGIN CERTIFICATE---` bis `---END CERTIFICATE---` und speichern Sie den Inhalt als neue Zertifikatsdatei mit der Erweiterung `.cer`.

2. Kopieren Sie die Zertifikatsdatei in das Verzeichnis `/nsconfig/ssl` in {{site.data.keyword.vpx_full}}.

<img src="images/11-transfer-certificate.png" alt="Zeichnung" style="width: 600px;"/>

{{site.data.keyword.vpx_full}} ist jetzt bereit, das Zertifikat mit SSL in eine Lastausgleichsbereitstellung zu integrieren.
