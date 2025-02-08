# Server Setup Instructions and Configuration

This document provides a detailed step-by-step guide to set up an Ubuntu Server virtual machine, configure its network, security, user management, services, database, WordPress, and backup systems according to the given specifications.

This project was made by Kaileen Umal (kumal) and Markus Tali (mtali)

---

## 1. The Virtual Machine Part

### Installing Ubuntu Server as a Virtual Machine

#### Setting hostname as {username}-host:

- Created a script file to set the hostname:
  sudo nano /usr/local/bin/set_hostname.sh

- Added the following script:

```bash
  USERNAME=$(whoami)

  NEW_HOSTNAME="${USERNAME}-host"

  sudo hostnamectl set-hostname "$NEW_HOSTNAME"

  echo "$NEW_HOSTNAME" | sudo tee /etc/hostname > /dev/null

  sudo sed -i "s/127.0.1.1 .\*/127.0.1.1 $NEW_HOSTNAME/" /etc/hosts
```

- Made the script executable:

```bash
  sudo chmod +x /usr/local/bin/set_hostname.sh
```

- Added the script to `/etc/profile` to run at each login:

```bash
  sudo nano /etc/profile
```

---

## 2. The Network Part

### Setting a Private IP Address with Netmask:

- Created a Netplan file:

```bash
  sudo nano /etc/netplan/00-installer-config.yaml
```

- Added the configuration:

```yaml
  network:
  version: 2
  renderer: networkd
  ethernets:
  enp0s3:
  dhcp4: no
  addresses: - 192.168.75.200/23 # The IP address of the server
  routes: - to: default
  via: 192.168.75.1 # IP address of the router found with `ip route | grep default`
  nameservers:
  addresses: - 8.8.8.8 # Google DNS
```

- Changed permissions for security:

```bash
  sudo chmod 600 /etc/netplan/00-installer-config.yaml
```

- Applied changes:

```bash
  sudo netplan apply
```

## 3. The Security Part

### SSH Configuration:

- Installed SSH server:

```bash
  sudo apt install openssh-server -y
```

- Edited SSH configuration:

```bash
  sudo nano /etc/ssh/sshd_config
```

- Updated settings:
  PermitRootLogin no
  Port 2222

- Applied changes:

```bash
  sudo systemctl restart sshd
```

### Configuring Firewall:

- Installed and enabled UFW:

```bash
  sudo apt install ufw
  sudo ufw default deny incoming
  sudo ufw default allow outgoing
  sudo ufw allow 2222/tcp
  sudo ufw enable
```

---

## 4. User Management Part

### Adding Users:

1. **luffy (Public Key Authentication, Sudoer):**

```bash
   sudo adduser luffy
   sudo usermod -aG sudo luffy
   sudo mkdir /home/luffy/.ssh
   sudo nano /home/luffy/.ssh/authorized_keys
```

- Pasted the public key into `authorized_keys`.

```bash
  sudo chmod 600 /home/luffy/.ssh/authorized_keys
  sudo chown -R luffy:luffy /home/luffy/.ssh
```

2. **zoro (Password Authentication, Non-Sudoer):**

```bash
sudo adduser zoro
```

---

## 5. Services Part

### Installing FTP Server:

- Installed `vsftpd`:

```bash
  sudo apt install vsftpd -y
```

- Edited the configuration:

```bash
  sudo nano /etc/vsftpd.conf
```

- Enabled the following:
  local_enable=YES
  write_enable=NO
  chroot_local_user=YES

- Created the `nami` user:

```bash
  sudo adduser nami
  sudo usermod -d /backup nami
```

- Restricted `nami` to `/backup`:

```bash
  sudo chown -R root:nami /backup
  sudo chmod 750 /backup
```

---

## 6. The Database Part

### MySQL Configuration:

- Installed MySQL:

```bash
  sudo apt install mysql-server -y
```

- Disabled remote root login by updating `/etc/mysql/my.cnf`:
  bind-address = 127.0.0.1

### WordPress Database Setup:

- Accessed MySQL:

```bash
  sudo mysql -u root
```

- Created WordPress database and user:

```sql
  CREATE DATABASE wordpress;
  CREATE USER 'wpuser'@'localhost' IDENTIFIED BY '1234';
  GRANT ALL PRIVILEGES ON wordpress.\* TO 'wpuser'@'localhost';
  FLUSH PRIVILEGES;
```

DB NAME = 'wordpress'
DB USER = 'wpuser'
DB PASSWORD = '1234'
DB HOST = 'localhost'

---

## 7. WordPress Part

### WordPress Installation:

- Downloaded WordPress:

```bash
  wget https://wordpress.org/latest.tar.gz
  tar -xzvf latest.tar.gz
  sudo mv wordpress /var/www/html
```

- Set permissions:

```bash
  sudo chown -R www-data:www-data /var/www/html/wordpress
  sudo chmod -R 755 /var/www/html/wordpress
```

- Secured `wp-config.php`:

```bash
  sudo mv /var/www/html/wordpress/wp-config-sample.php /var/www/html/wordpress/wp-config.php
  sudo chmod 600 /var/www/html/wordpress/wp-config.php
```

---

## 8. Backup Part

### Configuring Cron Job:

- Created backup script:

```bash
  sudo nano /usr/local/bin/backup.sh
```

Script content:

```yaml
#!/bin/bash
TIMESTAMP=$(date +%Y%m%d)
BACKUP_FILE="/backup/wp-database-$TIMESTAMP.tar.gz"
mysqldump -u wpuser -p'1234' wordpress > /tmp/wp-database.sql
tar -czvf $BACKUP_FILE /tmp/wp-database.sql
echo "Backup completed at $(date)" >> /var/log/backup.log
```

- Made the script executable:

```bash
  chmod +x /usr/local/bin/backup.sh
```

- Scheduled cron job:

```bash
  crontab -e
```

Cron entry:

```bash
0 0 \* \* \* /usr/local/bin/backup.sh
```

---

## 9. Q&a

### What is sudo group in Linux?

- The sudo group in Linux allows its members to run commands with root (admin) privileges using sudo. Users in this group can perform system tasks without logging in as root.

### What is a netmask?

- A netmask is a number that defines which part of an IP address belongs to the network and which part belongs to devices (hosts).

### Why is a static IP address important for a web server?

- A static IP keeps a web server's address constant, ensuring stable access, reliable domain mapping, and easier security setup. Without it, connections may break.

### What is an ssh server and what is the role of it?

- An SSH server allows secure remote access to a computer over a network. It lets users log in, run commands, and transfer files safely using encryption. It's mainly used for server management without needing physical access.

### What is a firewall and what is the role of it in a server?

- A firewall is a security system that controls incoming and outgoing network traffic on a server. It blocks unauthorized access while allowing safe connections, protecting the server from attacks.

### What is an FTP server and what is the role of it?

- An FTP server is a system that allows users to upload, download, and manage files over a network. It’s used for file sharing and storage, making it easy to transfer data between computers.

### What is a cron job and what is the role of it?

- A cron job is a scheduled task in Linux that runs automatically at set times. It's used for automation, like backups, updates, and system maintenance, without manual intervention.

### Why are backups important?

- Backups protect data from loss due to mistakes, hardware failures, or cyberattacks. They ensure you can restore important files and keep systems running smoothly.
