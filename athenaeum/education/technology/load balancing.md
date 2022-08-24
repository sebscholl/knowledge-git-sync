# Load Balancing

AWS SOLUTION (ELASTIC LOAD BALANCING - [https://aws.amazon.com/elasticloadbalancing/?nc2=type_a](https://aws.amazon.com/elasticloadbalancing/?nc2=type_a))

A Load balancer sits between the application servers and the request. Your app servers can have private IPs (not exposed to Public internet) while the Load Balancer is assigned a Public IP address. The load balancer then routes incoming traffic to an available application instance, using one of several different popular methods.

**Load Balancing Methods**

- Round Robin - MOST POPULAR, cycles between instances sequentially (simple and even distribution).
- Load Based - routes incoming requests to an instance with the lowest load.
    - Least connections approach
    - Resource-based (monitors machine for things like CPU, Memory, Disk space levels)
    

**Immediate Benefits**

- Scalability: Load balancing easily allows horizontal scaling of an application by creating new instances of the application behind the Load Balancer.
- Availability: Periodic health checks between the load balancer and application allow the load balancer to route traffic to healthy instances if certain servers crash.
- Convenience: Easy to redirect traffic using a single public-facing address.