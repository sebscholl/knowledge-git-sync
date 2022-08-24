202208241131

Status: #reference
Tags: [[servers & networking]]

# Setting up a remote SSH for Linux PC

### Installing SSH Server in Linux

```bash
sudo apt-get install openssh-server ii.
```

### Testing connection 
```bash
sudo service ssh status
# OR
ssh localhost
```

### Updating Config for Server
```bash
sudo vim /etc/ssh/sshd_config
```

Note that all changes require a server restart.

```bash
sudo service ssh restart
```

### Connecting via SSH

*Get IP address of localmachine using :*
```bash
ssh localhost

ip route

# IPs follow 'src' lines
# Example: ssh s@10.1.10.42
```

When connecting on remotely on same network, use Private IP, otherwise use Public IP.
___

[Guide for SSH Connection to Linux or Windows PC](https://phoenixnap.com/kb/ssh-to-connect-to-remote-server-linux-or-windows)