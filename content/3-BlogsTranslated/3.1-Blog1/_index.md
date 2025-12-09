---
title: "Blog 1"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AWS Site-to-Site VPN now supports IPv6 on external IP addresses

**By Ruskin Dantra, SaiJeevan Devireddy, and Scott Morrison**  
_September 24, 2025 – AWS Site-to-Site VPN, Networking & Content Delivery_

---

Amazon Web Services (AWS) Site-to-Site VPN is a fully managed service that enables you to create a secure connection between your data center or branch office and your AWS resources using IP Security (IPSec) tunnels. It provides critical connectivity for many types of workloads, including connecting on-premises workloads to the cloud, connecting devices to the cloud, and enabling encrypted communication.

Site-to-Site VPN is a flexible option for teams that need fast connectivity. When a VPN tunnel is configured, you must choose both external and internal IP addresses. IPv4 was the only option for both external and internal IP addresses until 2018, when AWS introduced support for IPv6 for internal IP addresses. In July 2025, AWS expanded this capability by announcing support for assigning IPv6 addresses to external IPs.

You can now connect IPv6 networks using Site-to-Site VPN connectivity with native IPv6 addresses, eliminating the need for IPv6 → IPv4 → IPv6 translation.

---

## Benefits of IPv6 support

- **Migration to IPv6**  
  This announcement enables a more straightforward transition to IPv6, allowing users to connect two IPv6 networks using only IPv6.

- **IPv4 address exhaustion**  
  Using IPv6 for outer tunnels helps conserve valuable IPv4 addresses in an environment where IPv4 has become scarce.

- **Cost reduction**  
  With IPv6 on external IPs, you can reduce the cost of connecting two networks without paying for public IPv4 addresses on either side of the tunnels (AWS side and on-premises side).

- **Regulatory and compliance requirements**  
  For regulated industries such as government, healthcare, finance, and telecommunications, IPv6 external addresses make it easier to meet requirements for IPv6-only networks.

---

## Supported configurations

IPv6 is supported only when Site-to-Site VPN terminates on an **AWS Transit Gateway** or an **AWS Cloud WAN core network edge (CNE)**. Figure 1 shows an example of an IPv6 Site-to-Site VPN terminating on a Transit Gateway.

**Figure 1: IPv6-only VPN connection to a Transit Gateway**

Terminating an IPv6 Site-to-Site VPN on a CNE follows the same model as shown above.

---

## IPv6 Site-to-Site VPN overview

To get started with an IPv6 Site-to-Site VPN, download the provided **AWS CloudFormation template** and deploy it in the AWS Region of your choice. The template requires only one parameter: an email address for notifications about potential outages. The template deploys the infrastructure shown in Figure 2 into your account.

**Figure 2: IPv6 Site-to-Site VPN CloudFormation deployment environment**

Deploying this template incurs costs, which are described in the **Cost** section. Refer to **Cleaning up** for teardown instructions. In the next sections, we describe the deployed infrastructure in detail.

---

## Simulated enterprise data center

To simulate an enterprise data center, the template deploys a VPC with the following infrastructure:

- An Amazon VPC configured as dual stack with one IPv4 prefix and one IPv6 prefix.
- The VPC IPv6 prefix can vary depending on whether you use AWS-provided IPv6 or Bring Your Own IP (BYOIP).
- An internet gateway attached to the VPC. This provides the VPN underlay and allows installation and configuration of the Amazon EC2 VPN router that simulates your on-premises router.
- Two IPv6-only public subnets that host the Amazon EC2 VPN router.
- An EC2 instance deployed in the IPv6-only public subnet to simulate the VPN router.
- Two public dual-stack subnets.
- Two NAT gateways deployed in those subnets to perform NAT64, allowing direct connectivity to the EC2 VPN router using AWS Systems Manager Session Manager. The NAT gateways are also required for CloudFormation to receive completion signals from `cfn-*` hooks.
- Two private dual-stack subnets for VPC endpoints that access other AWS services through AWS PrivateLink.
- Two IPv6-only private subnets to host test instances.
- An EC2 instance deployed in an IPv6-only private subnet to simulate a test instance.

---

## AWS infrastructure

The template terminates the IPv6 Site-to-Site VPN at a Transit Gateway and deploys the following infrastructure:

- A dual-stack Amazon VPC with one IPv4 prefix and one IPv6 prefix.
- Two private dual-stack subnets to host Transit Gateway attachments.
- A Transit Gateway with IPv6 support enabled.
- The VPC attached to the Transit Gateway, associated with the default route table, and configured to propagate routes to the default route table.
- Two IPv6-only private subnets that host test instances.
- An EC2 instance deployed in an IPv6-only private subnet to simulate a test instance.
- Two private dual-stack subnets that host VPC endpoints for accessing AWS services through AWS PrivateLink.
- An EC2 instance deployed in a dual-stack private subnet that acts as a jump box. This is required because this VPC does not have a NAT gateway for NAT64.

---

## Shared infrastructure

- **AWS Secrets Manager** for managing the VPN pre-shared key.
- **Amazon CloudWatch** for logs, metrics, and alarms.
- An **Amazon Simple Notification Service (Amazon SNS)** topic for outage notifications, such as tunnel-down events.
- An **AWS Key Management Service (AWS KMS)** customer managed key (CMK) to encrypt CloudWatch logs, Secrets Manager secrets, and the SNS topic.

---

## VPN infrastructure

The template also deploys the following VPN connectivity resources to build an IPv6 Site-to-Site VPN between the simulated on-premises data center and AWS:

- A customer gateway that logically represents your on-premises router.
- An IPv6 Site-to-Site VPN connection that terminates on the Transit Gateway.
- Configuration of the EC2 instance that simulates the router.

---

## IPv6 Site-to-Site VPN walkthrough

The following steps walk you through the IPv6 Site-to-Site VPN configuration.

### Prerequisites

Ensure the following before proceeding:

- The CloudFormation template has deployed successfully with no errors.

---

### Step 1: Customer gateway

1. Open the **Amazon VPC console** and navigate to  
   **Virtual private network (VPN) → Customer gateways**.

   **Figure 3: Navigate to customer gateways**

2. A customer gateway is already deployed for you. Creating a customer gateway for an IPv6 Site-to-Site VPN follows the same steps as for IPv4. The only difference is that it points to the IPv6 address of your router. In this case, it points to the IPv6 address of the EC2 instance simulating the VPN router.

   **Figure 4: AWS VPC Console – Customer Gateway view**

3. Navigate to the **Amazon EC2 console**, open **Instances**, and locate the instance named  
   `…-onprem-vpn/vpn-router-instance`. Its associated IPv6 address is displayed.

   **Figure 5: EC2 VPN router with IPv6 address**

---

### Step 2: IPv6 Site-to-Site VPN

The template also deploys an IPv6 Site-to-Site VPN connection.

**Figure 6: IPv6 Site-to-Site VPN details**

1. Open the **Amazon VPC console**.
2. In the navigation pane, choose **Virtual private network (VPN) → Site-to-Site VPN connections**.
3. Select the VPN connection created by the template named `…-vpn-connection`.
4. This connection has an associated **IPv6 customer gateway address**.
5. Navigate to the **Tunnel details** tab:
   - Two **IPv6 outside IP addresses**, one per tunnel.
   - Two `/126 IPv6 inside IP address prefixes`. These addresses are allocated from the `fd00::/8` range.
     - The first usable IPv6 address is on the AWS side.
     - The second usable IPv6 address is on your side.
     - Example: if the inside IPv6 prefix is `fd00:…:cd90/126`:
       - AWS side: `fd00:…:cd91`
       - On-premises side: `fd00:…:cd92`

IPv6 Site-to-Site VPN uses **dynamic routing** and advertises on-premises prefixes to AWS.  
You can observe the on-premises route (`2001:db8:0:0::/56`) propagated into the Transit Gateway route table via the Site-to-Site VPN attachment.

**Figure 7: On-premises route propagated to the Transit Gateway route table**

#### Verify routes on the AWS side

1. Open the **Amazon VPC console**.
2. In the navigation pane, choose **Transit gateways → Transit gateway route tables**.
3. Select the route table associated with the Transit Gateway created by the stack.
   - Use the CloudFormation output `AwsTransitGatewayId` to confirm the correct Transit Gateway.

#### Verify routes on the on-premises side

1. Open the **Amazon EC2 console**.
2. Select the instance named `…-onprem-vpc/vpn-router-instance`.
3. Choose **Connect**, then use **Session Manager** to connect.
4. Run the following command:

```bash
sudo vtysh -c "show ipv6 route bgp"
```
