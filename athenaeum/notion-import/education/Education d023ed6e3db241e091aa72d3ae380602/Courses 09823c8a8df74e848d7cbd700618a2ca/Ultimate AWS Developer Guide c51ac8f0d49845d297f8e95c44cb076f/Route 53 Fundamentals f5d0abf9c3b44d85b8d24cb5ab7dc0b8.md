# Route 53 Fundamentals

Created: May 8, 2019 1:34 PM
Updated: May 8, 2019 1:42 PM

AWS managed DNS service.

Most common record types:

- A: URL to IPv4
- AAAA: URL to IPv6
- CNAME: URL to URL
- Alias: URL to AWS resource

Usable domain types are:

- Public domains (ones you own or buy)
- Private domains (only resolvable within instance VPCs)

Advanced features include:

- Client side load balancing
- Limited health checks
- Routing policies
    - simple
    - failover
    - Geo-location
    - Geo-proximity
    - Latency
    - Weighted (x to Instance A and y...)

Always prefer an Alias vs a CNAME for any AWS resource.