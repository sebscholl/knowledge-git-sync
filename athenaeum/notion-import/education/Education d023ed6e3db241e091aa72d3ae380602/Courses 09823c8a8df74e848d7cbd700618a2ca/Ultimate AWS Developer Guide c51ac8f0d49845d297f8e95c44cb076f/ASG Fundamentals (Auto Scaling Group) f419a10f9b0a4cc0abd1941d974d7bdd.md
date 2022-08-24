# ASG Fundamentals (Auto Scaling Group)

Created: May 7, 2019 7:29 PM
Updated: May 7, 2019 7:59 PM

Allow EC2 instances to scale OUT for increased load and scale IN for decreased load by ADDING or REMOVING EC2 instances. This can be between a set min / max range, as well as set up to automatically assign added instances to a ELB (Load Balancer). When ASGs are provisioned with IAM roles, those are inherited by the EC2 instance. Additionally, ASGs can provision new instances in the event of failed health checks.

Params:

- Minimum Size (at least X always running)
- Actual / Desired (X running now)
- Maximum Size (at most X ever running)
- Launch config
    - AMI + Instance Type
    - EC2 User Data
    - EBS Volume
    - Security Groups
    - SSH Key Pair
- Network / Subnet Information
- Load Balancer Information

Auto Scaling Alarms are set in CloudWatch, which observes key metrics that dictate when Instances are added or removed (all metrics are calculated averages).

For example:

- Based on X CPU usage, I want to add / remove instances
- Custom metrics are available too (eg, number of connected users) using PutMetric API

ASGs are free (only charged for the resources).