Configuring a Hub-and-Spoke Architecture Using Azure Firewall
Project Overview

This project demonstrates how to design and implement a secure Hub-and-Spoke network architecture in Microsoft Azure using Azure Firewall. The architecture uses Windows Virtual Machines in both Hub and Spoke networks, with Azure Firewall deployed in the Hub Virtual Network to inspect and control traffic between the networks.

This architecture is commonly used in enterprise environments to centralize security, routing, and network management.

Architecture Diagram

Hub-and-Spoke network architecture:

                 +----------------------+
                 |     Hub VNet         |
                 |                      |
                 |  +---------------+   |
                 |  | Azure Firewall|   |
                 |  +-------+-------+   |
                 |          |           |
                 |   +------v------+    |
                 |   |  Hub VM     |    |
                 |   | (Jump Server)|   |
                 |   +-------------+    |
                 +----------+-----------+
                            |
                            | VNet Peering
                            |
                 +----------v-----------+
                 |     Spoke VNet       |
                 |                      |
                 |   +-------------+    |
                 |   |  Spoke VM   |    |
                 |   +-------------+    |
                 +----------------------+
Azure Resources Used
Resource	Name
Hub Resource Group	gowtham-hub-rg
Spoke Resource Group	gowtham-spoke-rg
Hub Virtual Network	hub-vnet
Hub Subnet	hub-subnet
Firewall Subnet	AzureFirewallSubnet
Hub VM	jump-server
Spoke Virtual Network	spoke-vnet
Spoke Subnet	spoke-subnet
Spoke VM	gowtham-spoke-vm
Azure Firewall	gowtham-azure-firewall
Project Architecture

The architecture consists of two main components:

1. Hub Network

The Hub Virtual Network acts as the central point for security and connectivity.

It contains:

Azure Firewall

Hub Virtual Machine (Jump Server)

Firewall subnet

Hub subnet

2. Spoke Network

The Spoke Virtual Network hosts the application workload.

It contains:

Spoke Virtual Machine

Spoke subnet

The Hub and Spoke VNets are connected using VNet Peering.

Implementation Steps
Step 1 – Create Hub Resource Group

Create a resource group for the Hub infrastructure.

Example:

Resource Group Name: gowtham-hub-rg
Region: East US (or preferred region)
Step 2 – Create Spoke Resource Group

Create a resource group for the Spoke resources.

Resource Group Name: gowtham-spoke-rg
Step 3 – Create Hub Virtual Network

Create the Hub Virtual Network with two subnets:

Hub Subnet

AzureFirewallSubnet (Required for Azure Firewall)

Example:

VNet Name: hub-vnet
Subnet:
  hub-subnet
  AzureFirewallSubnet
Step 4 – Create Spoke Virtual Network

Create the Spoke VNet with a subnet.

VNet Name: spoke-vnet
Subnet:
  spoke-subnet
Step 5 – Create Virtual Machines

Deploy two Windows virtual machines.

Hub VM
Name: jump-server
VNet: hub-vnet
Subnet: hub-subnet
Spoke VM
Name: gowtham-spoke-vm
VNet: spoke-vnet
Subnet: spoke-subnet
Step 6 – Deploy Azure Firewall

Deploy Azure Firewall in the Hub VNet.

Firewall Name: gowtham-azure-firewall
VNet: hub-vnet
Subnet: AzureFirewallSubnet

Azure Firewall will be used to inspect and control traffic between Hub and Spoke networks.

Step 7 – Configure VNet Peering

Create VNet peering between Hub and Spoke VNets.

Hub → Spoke Peering

Allow forwarded traffic

Allow gateway transit

Spoke → Hub Peering

Use remote gateway

This allows communication between the two networks through the Hub.

Step 8 – Configure Firewall Rules

Create firewall rules to control traffic.

Examples:

Allow RDP traffic

Allow ICMP or internal communication

Allow specific application traffic

This ensures secure and controlled network communication.

Security Benefits of Hub-and-Spoke Architecture

Centralized security using Azure Firewall

Reduced network complexity

Scalable architecture for multiple spokes

Improved traffic inspection

Better network segmentation

Use Cases

This architecture is widely used in:

Enterprise cloud networks

Multi-application environments

Secure hybrid cloud deployments

Centralized network security models

Tools & Services Used

Microsoft Azure

Azure Virtual Network

Azure Firewall

Windows Virtual Machines

VNet Peering

Resource Groups

Author

Kadali Gowtham Sai
