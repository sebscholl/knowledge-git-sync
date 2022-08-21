# ELB Fundamentals (Load Balancing)

Created: May 7, 2019 5:26 PM
Updated: May 7, 2019 5:46 PM

Think of a load balancer as a front to your application that allocates all incoming web traffic to your different instances / servers running downstream. Essentially, it brokers transactions between users and servers in order to optimize traffic flows (like the line queues at Whole Foods in Union Square).

The value of this is in allowing you to scale out your downstream services (multiple servers across an internal network) though still have one point of access to your application/service. Additionally, if a server fails the load balancer will redirect traffic to the running instances - through regular health checks.

ELB can provide an SSL or HTTPS connection between itself and the User, allowing it then to parlay the request to a given instance using HTTP protocol.

ELB can **enforce stickiness with cookies**, aka it will make sure that the same user is talking to the same running instance over time.

ELB can run across multiple availability zones.

EC2 Load Balancers are:

- Guaranteed by AWS to be working
- Taken care of by AWS for upgrades, maintenance and high availability
- Exposed to only a few user defined configurations
- Integrated with all AWS monitoring services

ELB Types:

- Classic V1 - 2009
- Application V2 - 2016
- Network V2 - 2017
- Recommended to use V2 by AWS