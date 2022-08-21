# EC2 Server Setup

Created: May 6, 2019 7:52 PM
Updated: May 7, 2019 7:45 PM

When SSH connected to instance.

*Connect via SSH

$ ssh -i <KEY_FILE>.pem ec2-user@<PUBLIC_IP>

1) Hop into root access user

$ sudo su

2) Update machine with latest packages (-y says YES to all updates)

$ yum update -y

3) Install HTTPd Apache hypertext transfer protocol server for x84-bit machine with 64-bit fallback ([https://httpd.apache.org/docs/2.4/programs/httpd.html](https://httpd.apache.org/docs/2.4/programs/httpd.html)).

$ yum install -y httpd.x86_64

4) Start Apache service

$ systemctl start httpd.service

5) Enable Apache server on device reboot.

$ systemctl enable httpd.service

6) Confirm everything is working using Apache test page at localhost:80

$ curl localhost:80

7) Add Hello World to default index.html file to serve page.

$ echo "Hello World from $(hostname -f)" > /var/www/html/index.html

Server Setup can be accomplished through the EC2 User Data script, which only runs when the instance is first created. It automates the boot task. The User Data Scripts automatically run as the root user.

```
#!/bin/bash
# Install Apache HPPTd on Linux 2 AMI
yum update -y
yum install -y httpd.x86_64
systemctl start httpd.service
systemctl enable httpd.service
echo "Hello World from $(hostname -f)" > /var/www/html/index.html
```

User data script gets Base64 encoded and passed to the machine.