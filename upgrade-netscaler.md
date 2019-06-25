---
copyright:
  years: 1994, 2018

lastupdated: "2018-11-12"

keywords: upgrade, vpx, callhome

subcollection: citrix-netscaler-vpx
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Upgrading your Citrix NetScaler VPX
{: #upgrading-your-citrix-netscaler-vpx}

You must be connected to the VPN before attempting this procedure.
{: note}

1. Log into NetScaler Management IP.
2. Click **System Upgrade**.
4. Choose **Local** from the **Choose File** drop-down list.
4. Download the correct upgrade file from the following location:

	[NetScaler Available Versions ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://downloads.service.softlayer.com/citrix/netscaler/){: new_window}

	You must be connected to the IBM© Cloud Infrastructure VPN in order to access this link.
  {: note}

5. On the Upload Software screen, browse to the location of the upgrade file and click **Upgrade**. The firmware will upload.
6. On the resulting System Upgrade window, you will be prompted to reboot. Click **Close**.
7. Go back to **System**, and click **Reboot**.
8. After the upgrade, close all browser instances and clear your computer's cache before accessing the appliance.


The user interface may differ depending on the current version of your NetScaler VPX.
{: note}

If you are upgrading from NetScaler version 11 to 12, the CallHome feature is enabled by default, even if you specifically disable it before and during installation. To disable this feature, you can either use the command line or the Citrix management UI:

   * Command line: `disable feature CallHome`
   * Citrix management UI:

     1. Navigate to **Configuration** > **System** > **Settings**.
     2. In the details pane, click **Configure Advanced features** link and uncheck the **Callhome** option.
     3. Click **OK**.
     {: note}
