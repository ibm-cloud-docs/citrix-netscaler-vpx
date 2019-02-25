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

# Create a Partition
{: #create-a-partition}

A partition is a logical and independent space that is associated or attached to the client requesting or creating cryptographic objects in the HSM engine. Each partition has its own data and policies isolated from other partitions. To learn more about partitions, refer to the [Administration Guide (page 211) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://public.dhe.ibm.com/cloud/bluemix/network/vpx/administration_guide.pdf){: new_window}. 

To create a partition, perform the following procedure:

1.	Login as the HSM Security Oficer/Administrator using the password specified during [initialization](/docs/infrastructure/citrix-netscaler-vpx?topic=citrix-netscaler-vpx-initialize-ibm-hardware-security-module-hsm-):
	
	```
	[jpmongehsm2] lunash:>hsm login
	
	Please enter the HSM Administrators' password: 
	> ********
	
	'hsm login' successful.
	
	Command Result : 0 (Success)
	```
	
2.	Confirm the HSM Admin Login Status is “Logged In”:
	
	```	
	[jpmongehsm2] lunash:>hsm show
	
	Appliance Details:
	==================
	Software Version:                6.2.2-5
	
	HSM Details: 
	============
	HSM Label:                          jpmonge
	Serial #:                           534071
	Firmware:                           6.10.9
	HSM Model:                          K6 Base
	Authentication Method:              Password
	HSM Admin login status:             Logged In
	HSM Admin login attempts left:      3 before HSM zeroization!
	RPV Initialized:                    No
	Audit Role Initialized:             No
	Remote Login Initialized:           No
	Manually Zeroized:                  No
	[OUTPUT OMITTED]
	```
	
	The output above should show `Logged In` in the HSM Admin login status. Otherwise, most operations and commands listed in the following sections will fail as they require administrator access. 

3.	List any existing partitions:
	
	```
	[jpmongehsm2] lunash:>partition list
	Storage (bytes)
	----------------------------
	Partition            Name                   Objects   	Total    Used    Free
	===================================
	534071016            partition1                   0  207559       0  207559 	534071020            partition2                   3  207559    3464  204095
	534071027            partition3                   0  207559       0  207559
	534071021            partition4                   2  207559    1652  205907
	534071030            partition5                  10  207559    9400  198159
	
	Command Result : 0 (Success)
	```
	
	This output shows five existing partitions.
	
4.	Create a new partition:
	
	**NOTE:** The password defined in this step will later be used to associate and create objects in the Citrix VPX HSM client process. Keep track of this password for later reference. Also, be sure to use the cloning domain defined during the initialization process.
	
	```
	[jpmongehsm2] lunash:>partition create -partition partition6
	
	On completion, you will have this number of partitions: 6
	
	-label:  Not provided; using name for label.
	
	Please enter a password for the partition:
	> **********
	
	Please re-enter password to confirm:
	> **********
	
	Please enter a cloning domain to use when creating this partition: 
	> ********
	
	Please re-enter cloning domain to confirm: 
	> ********
	
	Type 'proceed' to create the initialized partition, or 'quit' to quit now.
		> proceed
	'partition create' successful.
	
	Command Result : 0 (Success)
	```
	
	Where the syntax is:
	
	```
	partition create -partition <name-for-new-Partition>
	```
	
5.	Confirm the new partition was created:
	
	```
	[jpmongehsm2] lunash:>partition list
	
	Storage (bytes)	                                             	----------------------------
	Partition            Name                   Objects   Total    Used    Free
	===========================================
	534071016            partition1                   0  207559       0  207559
	534071020            partition2                   3  207559    3464  204095
	534071027            partition3                   0  207559       0  207559
	534071021            partition4                   2  207559    1652  205907
	534071030            partition5                  10  207559    9400  198159
	534071053            partition6                   0  207559       0  207559
	
	Command Result : 0 (Success)
	```
	
	The output of the `Partition List` command now shows six partitions.