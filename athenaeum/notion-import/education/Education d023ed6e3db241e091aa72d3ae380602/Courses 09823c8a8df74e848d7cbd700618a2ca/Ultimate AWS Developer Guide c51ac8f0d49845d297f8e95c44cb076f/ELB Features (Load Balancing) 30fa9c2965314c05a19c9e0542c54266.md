# ELB Features (Load Balancing)

Created: May 7, 2019 5:46 PM
Updated: May 7, 2019 6:05 PM

**Health Checks**

- Crucial for load balancers
- Allows ELB to know if an instance (EC2) is in service and not failing.
- Check is done on a custom port and route (usually port 4567 route /health)
- If response is not 200, considered unhealthy

**Application Load Balancers (v2)**

- Considered "Layer 7”
- Load balancing on multiple HTTP applications across machines (target groups)
- Load balancing on multiple applications on the same machines (containers)
- Load balance based our route in url
- Load balance based our hostname in url
- You can add stickiness to Target Groups based on hostnames and routes
- ALB supports HTTP(S) & Websocket protocols
- The Application servers (instances/target groups) never see the client IP
    - To access IP addresses, they are added to headers by the ALB as X-Forwarded-For
    - There are also:
        - X-Forwarded-Port
        - X-Forwarded-Proto
- GREAT for micro-services and container based applications
- Has port mapping to redirect to dynamic ports
- WITH CLASSIC load balancers you’d need to create one per application.

**Network Load Balancers (v2)**

- Forward TCP traffic to instances
- Handle millions of requests per second
- Support static and elastic IPs
- Less latency ~ 100ms (vs 400ms for ALB)
- Used for EXTREME performance
- Directly see the client IP
- They work the same way as the Application load balancers though using TCP protocol between the NLB and Target Groups

**Classic Load Balancers (v1)**

- Depreciated

*CLB and ALB support SSL certs and provide SSL termination

*All Load Balancers have health check capabilities

*All load balancers have static hostnames, not exposing the underlying IP

*Load balancers scale but not on demand, making you need to request it from AWS

- 4xx errors is from client
- 5xx errors is from application
- 503 means ELB is at capacity or has no registered target (instance)
- If the ELB cannot connect to the application, first check the security group!