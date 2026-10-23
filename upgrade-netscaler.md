---

copyright:
  years: 2017, 2026
lastupdated: "2026-10-23"

keywords: upgrade, callhome, ha, high availability, ha pair, cli

subcollection: citrix-netscaler-vpx
---

{{site.data.keyword.attribute-definition-list}}

# Upgrading your Citrix Netscaler VPX
{: #upgrading-your-citrix-netscaler-vpx}
{: help}
{: support}

You can upgrade your {{site.data.keyword.vpx_full}} to the most recent version by following the instructions here. This topic covers upgrading a standalone VPX and upgrading a High Availability (HA) pair, including the end-to-end UI and CLI procedures for downloading the firmware and upgrading the nodes.
{: shortdesc}

Before you upgrade, ensure that you meet the following prerequisites:

Failure to meet these prerequisites can cause a licensing issue with your Netscaler VPX, which can impact your productivity.
{: important}

* Ensure that your VPX administration passwords (`nsroot`, `root`) are up to date in the portal. For an HA pair, check the device passwords page in the {{site.data.keyword.cloud}} console for both NetScalers.
* Ensure that you are allowing any [Service Networks that are required for provisioning](/docs/infrastructure-hub?topic=infrastructure-hub-ibm-cloud-ip-ranges#service-network) through your gateway and server firewall so that firmware can be downloaded and NSE troubleshooting is possible if needed.
* Ensure that your license file is up to date through your VPX. For more information, see [Update your NetScaler license](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-transition-netscaler-to-las&interface=ui).
* Ensure that the `/var` partition has a minimum of 7 GB free (5 GB is the absolute minimum) and that the `/flash` partition has a minimum of 200 MB free. If you need to free up space, follow the recommendations in the **Cleaning Up /var on Netscaler ADC** guide.

## Upgrading a standalone VPX by using the UI
{: #gui-vs-cli-upgrade}

To upgrade your VPX by using the UI, follow these steps:

Be connected to the VPN before you attempt this procedure.
{: note}

1. Log in to NetScaler Management IP.
1. Click **System Upgrade**. The path is typically **Configuration > System upgrade**.
1. Choose **Local** from the **Choose File** menu list.
1. Download the correct upgrade file from the following location:
   * For commercial users: [NetScaler Available Versions](http://downloads.service.softlayer.com/citrix/netscaler/){: external}
   * For federal government users: [NetScaler Available Versions](http://downloads.service.usgov.softlayer.com/citrix/netscaler/){: external}

   Connect to the {{site.data.keyword.cloud}} Infrastructure VPN or from an {{site.data.keyword.cloud_notm}} Infrastructure server with private network (10.0.0.0/8) connectivity to access this link.
   {: note}

1. On the Upload Software screen, browse to the location of the upgrade file and click **Upgrade**. The firmware uploads.
1. On the resulting System Upgrade window, you are prompted to restart. Click **Close**.
1. Go back to **System**, and click **restart**.
1. After the upgrade, close all browser instances and clear your computer's cache.

The user interface might differ depending on the current version of your NetScaler VPX.
{: note}

This method is not recommended in {{site.data.keyword.cloud_notm}} environments. In {{site.data.keyword.cloud_notm}} environments, use the CLI procedure described in this topic instead.
{: important}

The UI upgrade spawns an SSH session that runs the same script as the CLI procedure, but it depends on continuous browser communication with the NetScaler. If you are connecting through a jumphost via SSL VPN or another private-network path, the session can time out and the upgrade appears hung. This is an issue observed particularly during 13.1 upgrades from earlier versions.

## Downloading the firmware to the NetScaler VPX
{: #download-firmware}

Firmware is hosted in {{site.data.keyword.cloud_notm}} repositories that are only reachable from endpoints with private-network connectivity (`10.0.0.0/8`) using {{site.data.keyword.cloud_notm}} Classic Infrastructure DNS:

- **Commercial:** `http://downloads.service.softlayer.com/citrix/netscaler/`
- **Federal (FedPod):** `http://downloads.service.usgov.softlayer.com/citrix/netscaler/`

DNS resolution of these FQDNs requires the standard {{site.data.keyword.cloud_notm}} Classic Infrastructure DNS resolvers (`10.0.80.11` / `10.0.80.12` for commercial; `100.100.100.80` / `100.100.100.81` for FedPod).

To download the firmware directly to the NetScaler:

1. Log in to the NetScaler via SSH from the appropriate jumphost in the same data center.

1. Switch to the install directory:

   ```sh
   shell
   cd /var/nsinstall
   ```
   {: pre}

1. List the available builds for your target version. For 13.1:

   ```sh
   curl --silent http://downloads.service.softlayer.com/citrix/netscaler/13.1/ \
     | grep -o 'href=".*">' | sed -e 's/href="//g' | sed -e 's/">//g'
   ```
   {: pre}

   Example output:
   ```
   ../
   build-13.1-17.42_nc_64.tgz
   build-13.1-21.50_nc_64.tgz
   build-13.1-37.38_nc_64.tgz
   build-13.1-49.13_nc_64.tgz
   build-13.1-49.15_nc_64.tgz
   build-13.1-51.15_nc_64.tgz
   build-13.1-53.17_nc_64.tgz
   build-13.1-53.23_nc_64.tgz
   build-13.1-53.24_nc_64.tgz
   build-13.1-57.26_nc_64.tgz
   build-13.1-59.19_nc_64.tgz
   build-13.1-59.22_nc_64.tgz
   build-13.1-60.26_nc_64.tgz
   build-13.1-60.32_nc_64.tgz
   build-13.1-61.23_nc_64.tgz
   build-13.1-61.26_nc_64.tgz
   build-13.1-62.23_nc_64.tgz
   build-13.1-63.16_nc_64.tgz
   build-13.1-63.18_nc_64.tgz
   build-13.1-63.21_nc_64.tgz
   build-13.1-64.22_nc_64.tgz
   build-13.1-64.24_nc_64.tgz
   build-13.1-64.28_nc_64.tgz
   build-13.1-64.29_nc_64.tgz
   ```

   For 14.1:

   ```sh
   curl --silent http://downloads.service.softlayer.com/citrix/netscaler/14.1/ \
     | grep -o 'href=".*">' | sed -e 's/href="//g' | sed -e 's/">//g'
   ```
   {: pre}

   Example output:
   ```
   ../
   build-14.1-47.46_nc_64.tgz
   build-14.1-47.48_nc_64.tgz
   build-14.1-60.52_nc_64.tgz
   build-14.1-60.58_nc_64.tgz
   build-14.1-66.54_nc_64.tgz
   build-14.1-66.59_nc_64.tgz
   build-14.1-72.57_nc_64.tgz
   build-14.1-72.61_nc_64.tgz
   build-14.1-73.33_nc_64.tgz
   build-14.1-73.37_nc_64.tgz
   build-14.1-73.41_nc_64.tgz
   build-14.1-73.46_nc_64.tgz
   ```

1. In this example, the latest 14.1 build is `build-14.1-73.46_nc_64.tgz`. Download the target build (replace the filename with the version you want):

   ```sh
   curl --output ./build-14.1-73.46_nc_64.tgz \
     http://downloads.service.softlayer.com/citrix/netscaler/14.1/build-14.1-73.46_nc_64.tgz
   ```
   {: pre}

   You should see a progress indicator similar to the following:

   ```
   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                    Dload  Upload   Total   Spent    Left  Speed
    90 1171M   90 1065M    0     0  81.2M      0  0:00:14  0:00:13  0:00:01 81.7M
   ```

   The download can take up to 15 minutes depending on the data center. This method is significantly faster than uploading through the UI.

## Installing the firmware by using the CLI
{: #upgrade-secondary-node}

The following procedure is generic and applies to both standalone and HA upgrades of the NetScaler VPX. Open console access for the VSI through {{site.data.keyword.cloud_notm}} classic infrastructure (IMS) on the appropriate Windows admin host before you begin, so you can monitor the reboot.

1. Log in to the node via SSH.

1. Navigate to the install directory:

   ```sh
   shell
   cd /var/nsinstall
   ```
   {: pre}

1. Confirm the downloaded firmware file is present by running `ls`.

1. Create a subdirectory, move the archive there, and change into it:

   ```sh
   mkdir build-14.1-73.46_nc_64
   mv build-14.1-73.46_nc_64.tgz ./build-14.1-73.46_nc_64/
   cd ./build-14.1-73.46_nc_64
   ```
   {: pre}

1. Extract the archive:

   ```sh
   tar -zvxf ./build-14.1-73.46_nc_64.tgz
   ```
   {: pre}

1. Run the installer:

   ```sh
   ./installns
   ```
   {: pre}

1. When prompted:
   ```
   Do you wish to delete old signature files and kernel images? [Y/N]
   ```
   Answer `Y` and press **Enter**.

1. After the installer finishes, you are prompted:
   ```
   Reboot NOW? [Y/N]
   ```
   Answer `Y` and press **Enter**. Switch to the console window to monitor the reboot. The upgrade is complete when the MOTD and login prompt appear on the console.

## Upgrading a Citrix Netscaler VPX HA pair
{: #upgrading-netscaler-ha-pair}

Upgrading a High Availability (HA) pair requires additional steps compared to a standalone upgrade, to ensure that no configuration is lost and that HA functionality is preserved throughout the process. Complete the prerequisites at the beginning of this topic for both nodes, and download the firmware as described in [Downloading the firmware to the NetScaler VPX](#download-firmware).

The IP addresses `10.72.164.206` (secondary) and `10.72.164.207` (primary) are used as examples. Substitute your own IP addresses.
{: note}

### HA pre-upgrade procedure
{: #ha-pre-upgrade}

Before upgrading either node, save the configuration, force a sync, and then disable propagation, sync, and failover on both nodes. This prevents configuration drift or an unintended failover while the two nodes are running different firmware versions.

The secondary (`10.72.164.206`) will be upgraded first, but the pre-upgrade commands must be run on the primary (`10.72.164.207`).

1. On the **primary** (`10.72.164.207`), save the configuration and force an HA sync:

   ```sh
   save ns config
   force ha sync
   ```
   {: pre}

   Both commands should return `Done.` if successful.

   `sync ha files all` is an alternative that explicitly synchronizes all SSL certificates, CRL lists, and VPN bookmarks. Because the primary is authoritative, this overwrites any differences on the secondary. Use it if you want to be certain the secondary is fully up to date.
   {: tip}

1. On the **primary** (`10.72.164.207`), lock the node as primary and disable propagation and sync:

   ```sh
   set ha node -hastatus StayPrimary
   set ha node -haprop Disabled
   set ha node -hasync Disabled
   ```
   {: pre}

1. On the **secondary** (`10.72.164.206`), also disable propagation and sync:

   ```sh
   set ha node -haprop Disabled
   set ha node -hasync Disabled
   ```
   {: pre}

1. Verify the HA state by running `sh ha node` and confirm that the settings are applied. Your configuration should reflect `StayPrimary` on the primary and propagation/sync disabled on both nodes before continuing.

### Upgrading the secondary node
{: #ha-upgrade-secondary-node}

Upgrade the secondary node (`10.72.164.206`) first by following the steps in [Installing the firmware by using the CLI](#upgrade-secondary-node).

### Making the upgraded secondary the new primary with HA force failover
{: #ha-force-failover}

Now that the secondary is upgraded, re-enable HA status on both nodes and fail over to make the upgraded node the new primary.

1. On the **current primary** (`10.72.164.207`), re-enable HA status:

   ```sh
   set ha node -hastatus enabled
   ```
   {: pre}

1. On the **current secondary** (`10.72.164.206`), re-enable HA status:

   ```sh
   set ha node -hastatus enabled
   ```
   {: pre}

1. On the **current primary** (`10.72.164.207`), initiate the failover:

   ```sh
   force ha failover
   ```
   {: pre}

   A warning about an **HA Version Mismatch** is expected at this point because the two nodes are running different firmware versions. When prompted `Please confirm whether you want force-failover (Y/N)? [N]:`, answer `Y`.

   The failover can be initiated from either node once `hastatus` is re-enabled on both.
   {: note}

1. After the failover, `10.72.164.206` is now the primary. Lock it as primary to prevent an unintended failover during the upgrade of the remaining node:

   ```sh
   set ha node -hastatus StayPrimary
   ```
   {: pre}

   This keeps the current primary running and prevents a failover from occurring during the upgrade of the remaining node.

1. Run `sh ha node` to confirm the new primary/secondary roles before proceeding.

### Upgrading the new secondary node
{: #upgrade-new-secondary}

Follow the same steps in [Installing the firmware by using the CLI](#upgrade-secondary-node) for the new secondary (`10.72.164.207`), substituting its IP address and using the same firmware file.

### HA post-upgrade procedure
{: #ha-post-upgrade}

After both nodes are running the same firmware version, re-enable HA and verify a clean failover.

1. On the **current primary** (`10.72.164.206`), re-enable all HA settings:

   ```sh
   set ha node -hastatus enabled
   set ha node -haprop enabled
   set ha node -hasync enabled
   ```
   {: pre}

1. On the **current secondary** (`10.72.164.207`), re-enable all HA settings:

   ```sh
   set ha node -hastatus enabled
   set ha node -haprop enabled
   set ha node -hasync enabled
   ```
   {: pre}

1. Run `sh ha node` to confirm both nodes show a healthy HA state with synchronization success.

1. Optionally, run `force ha failover` to return `10.72.164.207` to its original primary role.

## Disabling CallHome after upgrading from version 11 to 12
{: #disable-callhome}

If you are upgrading from NetScaler version 11 to 12, the CallHome feature is enabled by default, even if you specifically disable it before and during installation. To disable this feature, you can either use the command line or the Citrix management UI:

* Command line: `disable feature CallHome`
* Citrix management UI:

   1. Navigate to **Configuration** > **System** > **Settings**.
   1. In the details page, click **Configure Advanced features** link and clear the **CallHome** option.
   1. Click **OK**.
