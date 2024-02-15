---

copyright:
  years: 2019, 2020
lastupdated: "2020-09-09"

subcollection: citrix-netscaler-vpx

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when using Citrix Netscaler VPX
{: #vpx-responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.vpx_full}}. For a high-level view of the service types in {{site.data.keyword.Bluemix}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.vpx_full}}. For the overall terms of use, see [{{site.data.keyword.Bluemix}} Terms and Notices](/docs/overview?topic=overview-terms).

## Incident and operations management
{: #incident-and-ops}

Incident and operations management includes tasks such as monitoring, event management, high availability, problem determination, recovery, and full state backup and recovery.

|  | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Provision Citrix VPX| Ensuring that customer order is provisioned properly and in good condition  | Ensuring that the configuration was received|
|VPX environment monitoring| None  | Monitoring your environment |
|VPX design| None  | Designing and deploying your load balancing system, and engaging IBM for design consultation |
|VPX hardware/infrastructure failure| Monitoring and correcting all hardware and infrastructure failures | Notifying {{site.data.keyword.IBM_notm}} of hardware and infrastructure failures  |
{: row-headers}
{: caption="Table 1. Responsibilities for incidents and operations" caption-side="bottom"}

## Change management
{: #change-management}

Change management includes tasks such as deployment, configuration, upgrades, patching, configuration changes, and deletion.

|  | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|VM migration|  Ensuring that any migrations provide proper notification to customers  | Contacting {{site.data.keyword.IBM_notm}} if routine maintenance work should be scheduled on a different day |
|Upgrades| None  | Planning and implementing all upgrades |
|Configuration Modification| None | Providing subject matter expertise and modification of your environment |
{: row-headers}
{: caption="Table 2. Responsibilities for change management" caption-side="bottom"}

## Identity and access management
{: #iam-responsibilities}

Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access.

|  | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Initial root password| Ensuring that customers have IBM Cloud console access to initial root and nsroot passwords at provisioning | Notifying {{site.data.keyword.IBM_notm}} of any issues that are experienced during provisioning |
|All subsequent password changes| None  | Ensuring that root passwords remain consistent in the IBM Cloud console and on production systems |
|Account administration| None  | Designing and implementing VPX user account design goals |
{: row-headers}
{: caption="Table 3. Responsibilities for identity and access management" caption-side="bottom"}

## Security and regulation compliance
{: #security-compliance}

Security and regulation compliance includes tasks such as security controls implementation and compliance certification.

|  | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Critical Patch notification| Notifying customers of the need for critical patches through Event Management  | Implementing and applying the required patches |
{: row-headers}
{: caption="Table 4. Responsibilities for security and regulation compliance" caption-side="bottom"}

## Disaster recovery
{: #disaster-recovery}

Disaster recovery includes providing dependencies on disaster recovery sites, provisioning disaster recovery environments, data and configuration backup, replicating data and configuration to the disaster recovery environment, and failover on disaster events.

|  | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Backups| Applying customer backups during disaster recovery  | Keeping up-to-date backups of your current environment |
{: row-headers}
{: caption="Table 5. Responsibilities for disaster recovery" caption-side="bottom"}
