---

copyright:
  years: 2017, 2026
lastupdated: "2026-01-22"

keywords:

subcollection: citrix-netscaler-vpx

---

{{site.data.keyword.attribute-definition-list}}

# Initialize IBM Hardware Security Module (HSM)
{: #initialize-ibm-hardware-security-module-hsm-}

Most configurations of the HSM for your {{site.data.keyword.vpx_full}} require initialization of the HSM device. Without this, only certain `show` commands can be run.
{: shortdesc}

To initialize your device, follow these steps:

1. Connect by using SSH into the IBM© Hardware Security Module device with the credentials that are listed in the Control Portal under **Devices > Device List > Expand HSM name**.

   Alternatively, you can use public key authentication. For more information, review the [Appliance Administration Guide (page 38)](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/appliance_administration_guide.pdf){: external}.

   SSH access is enabled and allowed by default. If you have issues connecting with SSH, check your infrastructure routing and security.
   {: note}

2. Run the `hsm init` command:

    ```sh
    [jpmongehsm2] lunash:>hsm init -l jpmonge

    Please enter a password for the HSM Administrator:
    > ********

    Please re-enter password to confirm:
    > ********

    Please enter a cloning domain to use for initializing this HSM:
    > ********

    Please re-enter cloning domain to confirm:
    > ********

    CAUTION:  Are you sure you wish to initialize this HSM?

    Type 'proceed' to initialize the HSM, or 'quit'
        to quit now.
        > proceed
	  'hsm init' successful.

	  Command Result : 0 (Success)
    ```
    {: codeblock}

	Where the syntax used is: `hsm init -l <hsmlabel>`

The `-l` parameter or label is a parameter that is used to assign an identifier to the HSM, and can be any meaningful text or description that is related to the business, administrator, or the role it fulfills. The HSM administrator password is the designated password for the HSM Security Officer (SO). The SOd is essentially a profile that is required to create and configure crypto objects, as well as make changes to the HSM environment.

Lastly, the cloning domain is a shared identifier that allows objects to be formed among a group of HSMs. This mechanism is typically used for backup, HA or both.

Refer to the [LunaSH Command Reference Guide](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/lunash_command_reference_guide.pdf){: external} for all available commands supported in the HSM CLI.
