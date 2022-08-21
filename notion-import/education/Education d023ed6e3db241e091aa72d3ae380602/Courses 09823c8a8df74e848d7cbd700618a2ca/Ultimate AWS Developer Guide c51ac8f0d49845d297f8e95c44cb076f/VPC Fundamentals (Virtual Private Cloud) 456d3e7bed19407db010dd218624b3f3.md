# VPC Fundamentals (Virtual Private Cloud)

Created: May 8, 2019 3:53 PM
Updated: May 8, 2019 4:04 PM

Within a Region, you can create a VPC. VPCs are made up of subnets (networks) which are mapped to Availability Zones. All AWS accounts come with a default VPC, and it’s possible to connect to a VPC using a VPN.

- Public Subnet IPs are common, as well as Private Subnet IPs
- Having many subnets in AZs is common
- VPC are per Account per Region
- Subnets are per VPC per AZ
- Not all AWS resources can be deployed in a VPC

**Peer VPC**

Peer VPCs allow for VPCs to be connected (appear connected) across accounts

**Public Subnets**

Public Subnets usually contain the following resources:

- Load Balancers
- Static Websites
- Files
- Public Authentication Layers

**Private Subnets**

Private Subnets usually contain the following resources:

- Web app servers
- Databases

Differentiation is usually decided by, “What do I need to access over the web vs from a internal resource?"

**VPC Flow Logs**

Allow for monitoring of traffic within, in and out of VPC.

A public and private subnet can always communicate with one another when they are in the same VPC.