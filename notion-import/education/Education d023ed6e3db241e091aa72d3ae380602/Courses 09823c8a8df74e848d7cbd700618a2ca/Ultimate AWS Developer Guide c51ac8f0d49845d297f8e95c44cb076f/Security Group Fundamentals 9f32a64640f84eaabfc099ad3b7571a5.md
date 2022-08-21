# Security Group Fundamentals

Created: May 6, 2019 6:42 PM
Updated: May 6, 2019 6:53 PM

Security Groups are essentially firewalls around EC2 instances. They dictate what requests are allowed in and out. By default, no traffic is allowed in inbound and all traffic is allowed outbound. Things that can be controlled are ports, ip ranges and type, and any protocol for connection.

Security groups are scoped to regions, so each region that you’re operating in requires new security groups to be created. However, security groups can be shared across instances.

Additionally, any VPC requires its’ own security groups.

Timeouts are always security group issues.

Security groups can be nested, meaning that 1 Security group can “allow” several other security groups to connect to an EC2 instance. By doing this, you can easily allow instance to instance communication when other EC2 instances had the NESTED SECURITY GROUPS attached to them.