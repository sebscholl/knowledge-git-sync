# Networking Fundamentals (IPv4 vs IPv6)

Created: May 6, 2019 6:54 PM
Updated: May 6, 2019 7:45 PM

Private vs Public IPs.

There are two types of IP’s.

IPv4 ([0-255].[0-255].[0-255].[0-255])

IPv6. (0000:0000:0:000:0000:0000:0000)

IPv4 is most common web IP type while IPv6 is more common for IoT devices. The IPv4 allows for 3.7 billion unique server addresses in the public space.

Servers with Public IPs are able to communicate via web protocol to one another. Whereas the private networks use Private IP’s. The private networks can have public gateways through which www connections can take place. However, within the private network machines are only able to communicate with one another.

In short:

Public IP:

- accessible over the internet
- IP
    
    unique across the web
    
- Can be geo-located easily

Public IPs will change when instances are stopped and restarted.

Private IP:

- accessible within Private Network
- IP unique within private network
- Only specific range of IPs are paid IPs

Public IPs will NOT change when instances are stopped and restarted.

AWS offers Elastic IPs which are server addresses you own until you delete them. They are public IP addresses. However, the value of them is that they can be programmatically remapped to different instances (in the event of failure, per say).

AWS limits you to 5 Elastic IP addresses.

According to Meerek, Elastic IPs usually reflect poor architecture decisions. It is better to go with one of the following options.

1) Map DNS to public IP

2) Use Load Balancing