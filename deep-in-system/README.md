1. The Virtual Machine Part:

2. The Network Part:

Setting a private IP address with netmask:

- Created a netplan file using `sudo nano /etc/netplan/00-installer-config.yaml`
- Added the following lines to the file:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        - 192.168.1.100/24 # The ip address of the server
      routes:
        - to: default
          via: 10.0.2.2 # The ip address of the router that was found with `ip route | grep default`
      nameservers:
        addresses:
          - 8.8.8.8 # Google
```

- Changed the files permissions so only the root can read and write, with: `sudo chmod 600 /etc/netplan/00-installer-config.yaml`

- Applied all of the changes with: `sudo netplan apply`

Now the server has a static ip address (192.168.1.100/24)

![picture](/pictures/showingIpAddress.png)

Pinging Google is successful

![picture](/pictures/pingingGoogle.png)

3. The security part
