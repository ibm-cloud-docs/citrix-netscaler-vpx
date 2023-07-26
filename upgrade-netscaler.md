---
copyright:
  years: 1994, 2019

lastupdated: "2019-11-12"

keywords: upgrade, callhome

subcollection: citrix-netscaler-vpx
---

{{site.data.keyword.attribute-definition-list}}

# Upgrading your Citrix Netscaler VPX
{: #upgrading-your-citrix-netscaler-vpx}
{: help}
{: support}

You can upgrade your {{site.data.keyword.vpx_full}} to the most recent version by following the instructions here.
{: shortdesc}

Before attempting to upgrade, ensure that the following prerequisites have been met.  

Failure to meet these prerequisites may cause a licensing issue with your Netscaler VPX, which can impact your productivity.
{: important}

* Ensure that your VPX administration passwords are up to date in the portal.
* Ensure that you are allowing any [Service Networks required for provisioning](/docs/cloud-infrastructure?topic=cloud-infrastructure-ibm-cloud-ip-ranges#service-network) through your gateway and server firewall.
* Ensure that your license file is up-to-date through your VPX. If not, you can update it by [opening a support case](https://cloud.ibm.com/unifiedsupport/cases/form){: external}.

To upgrade your VPX, perform the folllowing proedure:

You must be connected to the VPN before attempting this procedure.
{: note}

1. Log into NetScaler Management IP.
1. Click **System Upgrade**.
1. Choose **Local** from the **Choose File** menu list.
1. Download the correct upgrade file from the following location:
   * For commercial users: [NetScaler Available Versions](http://downloads.service.softlayer.com/citrix/netscaler/){: external}
   * For federal government users: [NetScaler Available Versions](http://downloads.service.usgov.softlayer.com/citrix/netscaler/){: external}

   You must be either connected to the {{site.data.keyword.cloud}} Infrastructure VPN or connecting from an {{site.data.keyword.cloud_notm}} Infrastructure server with private network (10.0.0.0/8) connectivity in order to access this link.
   {: note}

1. On the Upload Software screen, browse to the location of the upgrade file and click **Upgrade**. The firmware uploads.
1. On the resulting System Upgrade window, you will be prompted to reboot. Click **Close**.
1. Go back to **System**, and click **Reboot**.
1. After the upgrade, close all browser instances and clear your computer's cache before accessing the appliance.


The user interface might differ depending on the current version of your NetScaler VPX.
{: note}

If you are upgrading from NetScaler version 11 to 12, the CallHome feature is enabled by default, even if you specifically disable it before and during installation. To disable this feature, you can either use the command line or the Citrix management UI:

* Command line: `disable feature CallHome`
* Citrix management UI:

1. Navigate to **Configuration** > **System** > **Settings**.
2. In the details pane, click **Configure Advanced features** link and uncheck the **CallHome** option.
3. Click **OK**.
