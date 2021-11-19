---

copyright:
  years: 2019
lastupdated: "2019-11-13"

keywords: ipsec, vpn, tunnel

subcollection: citrix-netscaler-vpx


---

{{site.data.keyword.attribute-definition-list}}

# Configuring the Virtual Router Appliance
{: #configuring-vra}

Now that your {{site.data.keyword.vpx_full}} is configured, you need to configure the IBM Virtual Router Appliance (VRA).
{: shortdesc}

To do this, use the following syntax:

   ```sh
   set security vpn ipsec esp-group ESP lifetime '86400'
   set security vpn ipsec esp-group ESP mode 'tunnel'
   set security vpn ipsec esp-group ESP pfs 'disable'
   set security vpn ipsec esp-group ESP proposal 1 encryption 'aes256'
   set security vpn ipsec esp-group ESP proposal 1 hash 'sha1'
   set security vpn ipsec ike-group IKE lifetime '86400'
   set security vpn ipsec ike-group IKE proposal 1 dh-group '2'
   set security vpn ipsec ike-group IKE proposal 1 encryption 'aes256'
   set security vpn ipsec ike-group IKE proposal 1 hash 'sha1'
   set security vpn ipsec site-to-site peer 10.143.220.106 authentication mode 'pre-shared-secret'
   set security vpn ipsec site-to-site peer 10.143.220.106 authentication pre-shared-secret 'ipsecpskvpxvra'
   set security vpn ipsec site-to-site peer 10.143.220.106 connection-type 'initiate'
   set security vpn ipsec site-to-site peer 10.143.220.106 default-esp-group 'ESP'
   set security vpn ipsec site-to-site peer 10.143.220.106 ike-group 'IKE'
   set security vpn ipsec site-to-site peer 10.143.220.106 local-address '10.115.168.144'
   set security vpn ipsec site-to-site peer 10.143.220.106 tunnel 1 local prefix '10.115.72.192/26'
   set security vpn ipsec site-to-site peer 10.143.220.106 tunnel 1 remote prefix '192.168.0.0/24'
   ```
   {: codeblock}
