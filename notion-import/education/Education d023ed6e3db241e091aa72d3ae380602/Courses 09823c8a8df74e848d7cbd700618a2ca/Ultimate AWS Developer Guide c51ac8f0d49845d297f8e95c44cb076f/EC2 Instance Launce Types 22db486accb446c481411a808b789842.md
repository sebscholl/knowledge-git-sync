# EC2 Instance Launce Types

Created: May 6, 2019 8:24 PM
Updated: December 19, 2019 10:56 PM

On Demand Instances

- Good for short workloads with predictable pricing.

Reserved Instances:

- Up to 75% cheaper than onDemand!
- Long workloads (database…)
- Convertible Reserved Instances:
    - Long workloads with flexible instances, allowing for jumping between instance types.

> 
> 
- Scheduled Reserve Instances:
    - Launches within a specific time window on a repeating schedule

Spot Instances:

- Up to 90% discount
- Acquired through bidding process, and can loose instance when outbid
- 2-minute notification that you’ve been outbid
- Good for batch jobs, big data analysis, workloads that can fail

Dedicated Host:

- Actually physical server with full control of EC2 Instance Placement
- Access to underlying sockets and physical core drives
- It is registered on a 3-year contract and the most expensive option
- (Need for BYOL - Bring Your Own License - requirement or other regulatory issues)

Dedicated Instance:

- Running instance on hardware that is dedicated to you.
- All instances launched from account are launched on hardware dedicated to you
- No control over instance (if started and stoped instance could move between hardware).