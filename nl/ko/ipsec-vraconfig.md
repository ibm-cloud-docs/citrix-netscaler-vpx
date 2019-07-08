---

copyright:
  years: 2019
lastupdated: "2019-04-28"

keywords: ipsec, vpn, vpx, tunnel

subcollection: citrix-netscaler-vpx


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:note: .note}
{:important: .important}

# 가상 라우터 어플라이언스 구성
{: #configuring-vra}

이제 Citrix VPX가 구성되었으므로 IBM Virtual Router Appliance(VRA)를 구성해야 합니다. 이를 수행하려면 다음 구문을 사용하십시오.   

  ```
  
  $ set security vpn ipsec esp-group ESP lifetime '86400'
  $ set security vpn ipsec esp-group ESP mode 'tunnel'
  $ set security vpn ipsec esp-group ESP pfs 'disable'
  $ set security vpn ipsec esp-group ESP proposal 1 encryption 'aes256'
  $ set security vpn ipsec esp-group ESP proposal 1 hash 'sha1'
  $ set security vpn ipsec ike-group IKE lifetime '86400'
  $ set security vpn ipsec ike-group IKE proposal 1 dh-group '2'
  $ set security vpn ipsec ike-group IKE proposal 1 encryption 'aes256'
  $ set security vpn ipsec ike-group IKE proposal 1 hash 'sha1'
  $ set security vpn ipsec site-to-site peer 10.143.220.106 authentication mode 'pre-shared-secret'
  $ set security vpn ipsec site-to-site peer 10.143.220.106 authentication pre-shared-secret 'ipsecpskvpxvra'
  $ set security vpn ipsec site-to-site peer 10.143.220.106 connection-type 'initiate'
  $ set security vpn ipsec site-to-site peer 10.143.220.106 default-esp-group 'ESP'
  $ set security vpn ipsec site-to-site peer 10.143.220.106 ike-group 'IKE'
  $ set security vpn ipsec site-to-site peer 10.143.220.106 local-address '10.115.168.144'
  $ set security vpn ipsec site-to-site peer 10.143.220.106 tunnel 1 local prefix '10.115.72.192/26'
  $ set security vpn ipsec site-to-site peer 10.143.220.106 tunnel 1 remote prefix '192.168.0.0/24'
  
  ```
  {: codeblock}
