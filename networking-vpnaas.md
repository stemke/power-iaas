﻿---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-27"

keywords: network vpnaas, ipsec, ike, juniper, cisco, vlan, strongswan

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Understanding VPN-as-a-service (VPNaaS) for Power Systems Virtual Servers (beta)
{: #understanding-vpnaas}

With the {{site.data.keyword.powerSysShort}} service's virtual private network (VPN), you can connect an on-premises VPN gateway to an {{site.data.keyword.cloud}} VPN (the {{site.data.keyword.powerSys_notm}}) VPN gateway is pre-creatd and shares the necessary IPs).
{: shortdesc}

The {{site.data.keyword.powerSys_notm}} infrastructure consists of subnets and virtual server instances (VSIs). The {{site.data.keyword.powerSys_notm}} VPN gateway establishes an IPsec site-to-site link to an on-premises VPN gateway.

The IPsec and the Internet Key Exchange (IKE) protocols are proven open standards for secure communication.
{: note}

There are many popular on-premises VPN solutions that are available for site-to-site gateways. You can get IPsec VPN solutions from companies like Cisco and Juniper or choose an open source IPsec-based VPN solution like strongSwan.

In short, you can use a VPN to:

- Connect your on-premises systems to services and workloads that are running in the {{site.data.keyword.cloud_notm}}.
- Ensure a dedicated private and low-cost stable alternative to internet-based connectivity to {{site.data.keyword.cloud_notm}} services.
- Connect your IBM cloud-based systems to services and workloads that are running on-premises.

In the following graphic, you'll see that:

- The IPSec tunnel end-point is in the VPN gateway and is reachable from the internet via the IBM Cloud network.
- The customers private networks to the customer on-premises network are routed via the IPsec tunnel.

  ![Power Systems Virtual Server VPNaaS](./images/diagram-vpnaas.png "Power Systems Virtual Server VPNaaS"){: caption="Figure 1. Power Systems Virtual Server VPNaaS" caption-side="bottom"}

Example network configuration:

```
Customer VM Subnet1: 172.32.0.0/28   VLAN: 300
Customer VM Subnet1: 172.10.0.0/28   VLAN: 301
IPSec Tunnel Subnet: 100.64.64.0/30
IPSec VPN Gateway IP: 161.100.1.50 (Public IP)
Customer on-prem IPsec Gateway: 162.20.20.1
```

## Requesting and configuring VPNaaS
{: #configuring-vpnaas}

To request and configure your VPN, complete the following steps:

The {{site.data.keyword.powerSys_notm}} VPNaaS offering is in **beta**. You must open a support ticket to activate this offering. The official VPNaaS release will include user interface (UI) and command-line interface (CLI) support.
{: preview}

1. You can use VPNaaS with your existing VSIs and private networks. If you haven't created at least one VSI or private network, see [Creating a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) and [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).

2. Open a support ticket against the {{site.data.keyword.powerSys_notm}} service to request a VPN connection. Follow the support ticket process that is described at [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

3. In the subject field of the support ticket, enter the following (replacing the location with your own):

    Power Systems Virtual Server VPNaaS Beta Setup - Location: FRA04
    {: codeblock}

4. In the support ticket description field, provide the following information for your network:

    1. **Gateway IP**
    2. **Connection name**
    3. **Subnets to be reached at your location (in CIDR notation)**
    4. **Subnets to be reached in the Power Systems Virtual Server environment (in CIDR notation)**

5. The {{site.data.keyword.powerSys_notm}} side of the VPN is configured after the {{site.data.keyword.powerSys_notm}} team gets the request. After the initial configuration, the {{site.data.keyword.powerSys_notm}} team sends you the following network information to complete the configuration on your network:

    1. **Power VS Gateway IP**
    2. **Power VS IPsec Policy**
    3. **Shared secret key (provided to the authorized recipient)**
    4. **Local Identity IP**
    5. **Remote Identity IP**
    6. **GRE Tunnel IP**
    7. **GRE Tunnel Source IP (Loop back IP configured in your firewall)**
    8. **GRE Tunnel Destination IP**

6. The {{site.data.keyword.powerSys_notm}} team configures routes to reach your on-premises subnets, thus making your {{site.data.keyword.powerSys_notm}} reachable from the on-premises assets that are using the VPNaaS service.

7. The {{site.data.keyword.powerSys_notm}} team tests connectivity and provides the results in the original support ticket.

8. The support ticket is closed when you confirm that the VPN is working.
