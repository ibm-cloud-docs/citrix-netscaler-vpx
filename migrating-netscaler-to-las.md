---
copyright:
  years: 2017, 2026
lastupdated: "2026-01-23"

keywords: order, citrix, vpx, overview

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Action required: Update your NetScaler license
{: #transition-netscaler-to-las}

Citrix is retiring file‑based licensing effective 10 April 2026, and replacing it with the cloud‑based License Activation Service (LAS). All NetScaler VPX instances running on IBM Cloud Classic infrastructure must transition to LAS to remain licensed, compliant, and supported.
{: shortdesc}

The following information provides guidance for provisioning new or reloaded NetScaler instances, renewing annual LAS licenses, and transitioning existing VPX appliances from file-based licensing to LAS. To enable LAS, IBM Support activates the required Citrix Cloud components on your behalf.

As you plan your upgrade, consider the following service impacts:

* The required actions will require appliance reboots, resulting in temporary service disruption.
* The update can't be performed on a live system and must be completed during a scheduled maintenance window.
* Completing the licensing transition requires coordination between your appliance administrator and IBM Support to exchange the information that is needed to generate the new licensing data.

Customers are strongly encouraged to begin planning for the required maintenance window and associated downtime as early as possible.
{: note}

## Key milestones
{: #milestones}

Complete the following milestones before 10 April 2026 to help ensure uninterrupted license validation and continued support. You can start milestone 2 immediately after completing milestone 1.

* **Milestone 1**: Starts 26 January 2026

   [Upgrade to the minimum supported software version](#upgrade-to-minimum-supported-software-version)

* **Milestone 2**: Ends 10 April 2026

   [Install and activate the new VPX license activation file (blob)](#transition-netscaler-to-las-ui){: ui}

   [Install and activate the new VPX license activation file (blob)](#transition-netscaler-to-las-cli){: cli}

Starting 2 February 2026, IBM will open a separate support case for each VPX instance that you own. To complete the LAS transition, you must use these support cases to submit your NetScaler activation request files and receive the corresponding license activation files from IBM Support.
{: important}

To view support cases, log in to the IBM Support site at [https://ibm.com/mysupport](https://ibm.com/mysupport){: external} and click **Cases > View your cases**. 
{: tip}

## Milestone 1: Upgrading to the minimum supported software version
{: #upgrade-to-minimum-supported-software-version}

Your VPX must run one of the following software versions or later. Appliances running earlier versions cannot install or validate the new license activation file.

- NetScaler 14.1: Version 14.1 build 51.80 or later
- NetScaler 13.1: Version 13.1 build 60.29 or later
- NetScaler 13.1: Version 13.1 build 37.247 (FIPS) or later

If your NetScaler appliance doesn't meet these requirements, upgrade before activating LAS. For more information, see [Upgrading your Citrix Netscaler VPX](/docs/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-upgrading-your-citrix-netscaler-vpx).
{: attention}

Your administrator must:

* Confirm the current software version
* Perform the upgrade, including any required reboots
* Validate system operation post-upgrade

## Milestone 2: Installing and activating the new VPX license activation file in the GUI
{: #transition-netscaler-to-las-ui}
{: ui}

To transition NetScaler licensing in the NetScaler ADC GUI:

1. Log in to the NetScaler ADC GUI.
1. Browse to **System > Licenses > ADC License**, then click **LAS Offline Activation**.

   This action generates an activation request file, which contains unique identity information for the NetScaler instance.

1. In the **Generate NetScaler offline activation request file** section, click **Generate**.
1. After the file is generated, click **Download** to save it to your local system.

   The activation request file expires after 7 days.
   {: important}

1. Request a license activation file for your NetScaler. To do so, open the IBM-generated support case titled "VPX License Transition" and provide the following information:

   * Subject: LAS Transition
   * VPX instance details, such as your NetScaler IP, version, hostname, and serial if available.
   * Attach the LAS activation request file that you generated.

   IBM Support registers the NetScaler with Citrix, obtains a license activation file, and attaches the activation file to your support case.

   The activation file expires after 1 year.
   {: note}

1. Upload the LAS activation file:

   1. Return to the NetScaler ADC GUI (**System > Licenses > ADC License**, then click **LAS Offline Activation**).
   1. In the **Upload NetScaler activation file** section, click **Upload File**.
   1. Select the activation file that you received from IBM Support.
   1. Click **Yes** to confirm the activation.
   1. If prompted, click **Reboot** for the license to take effect.

      A reboot isn't required in the following scenarios:
        * You are switching from file-based licensing to LAS and the entitlement remains unchanged.
        * You are renewing an existing LAS license and the entitlement remains unchanged.

1. To verify license activation, go to **System > Licenses**.

## Milestone 2: Installing and activating the new VPX activation file from the CLI
{: #transition-netscaler-to-las-cli}
{: cli}

To install and activate the new VPX activation file from the NetScaler CLI, follow these steps:

1. To generate the LAS activation request file (blob), enter the following command:

   ```sh
   show ns licenseactivationdata
   ```
   {: pre}

1. The generated activation file appears in the following path:

   ```sh
   /nsconfig/license/<FileName>
   ```
   {: pre}

1. Copy the activation file from NetScaler to your local system by using the Secure Copy command (SCP).

   ```sh
   scp nsroot@<NSIP>:/nsconfig/license/NS_activation_blob.tgz .
   ```
   {: pre}

   The activation request file expires after 7 days.
   {: note}

1. Open the IBM-generated support case titled "VPX License Transition" and provide the following information:

   * Subject: LAS Transition
   * VPX instance details, such as NetScaler IP, version, hostname, and serial if available.
   * Attach the activation request file that you generated.

   IBM Support registers the request in Citrix Cloud LAS, generates the LAS activation file, and provides it to you through your IBM Support case.

   The activation file expires after 1 year. Complete the activation within this time frame. If the activation file expires, the VPX becomes unlicensed and can stop traffic processing.
   {: note}

1. To upload the activation file that you receive from IBM Support, enter the following commands:

   ```sh
      # Copy the activation file from your local system to the following NetScaler directory
   scp NS_activation_blob.tgz nsroot@<NSIP>:/nsconfig/license
   ```
   {: pre}

    ```sh
      # Run the following command to activate the license on your NetScaler
   apply ns laslicense -filename NS_activation_blob.tgz -filelocation /nsconfig/license -fixedBandwidth
   ```
   {: pre}

1. Reboot the device if prompted.

   A reboot isn't required in the following scenarios:
     * You are switching from file-based licensing to LAS and the entitlement remains unchanged.
     * You are renewing an existing LAS license and the entitlement remains unchanged.

1. To verify LAS licensing, enter the following commands:

   ```sh
   show ns license
   ```
   {: pre}

   ```sh
   show ns laslicense
   ```
   {: pre}

## Renewing your annual license
{: #monitor-renew-license}

The license activation file is valid for one year. Follow these steps to monitor and renew your license:

1. In the NetScaler licensing GUI, go to **System > Licenses** to view:{: ui}

   * The last activation or renewal date{: ui}
   * Upcoming activation or renewal date{: ui}

1. To make sure NetScaler operations remain uninterrupted, follow these steps before the renewal date:{: ui}

   1. Click **Renew now** before the renewal date.{: ui}
   1. Generate a new activation request file. For instructions, see steps 1-4 in [Installing and activating the new VPX license token](#transition-netscaler-to-las-ui).{: ui}
   1. Open the IBM-generated support case titled "VPX License Transition" and request a license activation file (see step 5).{: ui}
   1. Upload the new LAS activation file from IBM Support (see step 6).{: ui}

1. To monitor the license activation file and apply a new file before it expires, enter the following command: {: cli}

   ```sh
   show ns laslicense
   ```
   {: pre}
   {: cli}

   The command output displays the LAS license details including activation and renewal dates.
   {: cli}

1. Generate the LAS activation request file. For instructions, see steps 1-3 in [Installing and activating the new VPX activation file from the CLI](#transition-netscaler-to-las-cli).{: cli}
1. Open the IBM-generated support case titled "VPX License Transition" and request a license activation file (see step 4).{: cli}
1. Upload the new LAS activation file from IBM Support (see step 5).{: cli}
