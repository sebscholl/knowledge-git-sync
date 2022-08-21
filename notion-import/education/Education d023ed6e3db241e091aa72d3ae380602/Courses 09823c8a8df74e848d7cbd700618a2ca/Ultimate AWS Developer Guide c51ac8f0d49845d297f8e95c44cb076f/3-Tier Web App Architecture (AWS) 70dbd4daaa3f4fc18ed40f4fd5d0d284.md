# 3-Tier Web App Architecture (AWS)

Created: May 8, 2019 4:05 PM
Updated: May 8, 2019 5:13 PM

![3-Tier%20Web%20App%20Architecture%20(AWS)%2070dbd4daaa3f4fc18ed40f4fd5d0d284/Screen_Shot_2019-05-08_at_4.05.28_PM.png](3-Tier%20Web%20App%20Architecture%20(AWS)%2070dbd4daaa3f4fc18ed40f4fd5d0d284/Screen_Shot_2019-05-08_at_4.05.28_PM.png)

In the typical 3-tiew web app architecture on AWS, we can see a number of services coming together.

1) User hits domain name and Route 53 returns server (ALB) IP address.

2) Application Load Balancer takes request and routes it to an application instance (EC2 M3 instances) which is contained within an ASG that is split between multiple AZs.

3) The ALB is contained in a Public Subnet and ASG in a Private Subnet. Both of which are able to talk to each other as they are in the same region.

4) Any DB reads are parlayed to the ElastiCache instance, which either returns a “Cache Hit/Miss”. In which case, if needed, the application can then connect directly to an RDS DB to query or write any data.

5) The RDS instance has a cross region synchronous standby DB, protecting against the change of failure.