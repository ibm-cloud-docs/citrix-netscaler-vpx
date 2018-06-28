---
copyright:
  years: 1994, 2018

lastupdated: "2018-06-28"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Upgrade your Citrix NetScaler VPX

**NOTE:** You must be connected to the VPN before attempting this procedure.

1. Log into NetScaler Management IP.
2. Click **System Upgrade**.
4. Choose **Local** from the **Choose File** drop-down list. 
4. Download the correct upgrade file from the following location:

	[NetScaler Available Versions ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://downloads.softlayer.local/citrix/netscaler/){: new_window}
	**NOTE:** You must be connected to the IBM Cloud Infrastructure VPN in order to access this link.

5. On the Upload Software screen, browse to the location of the upgrade file and click **Upgrade**. The firmware will upload.
6. On the resulting System Upgrade window, you will be prompted to reboot. Click **Close**.
7. Go back to **System**, and click **Reboot**.
8. After the upgrade, close all browser instances and clear your computer's cache before accessing the appliance.

**NOTE:**: The user interface may differ depending on the current version of your NetScaler VPX.



