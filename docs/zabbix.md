**SETUP**

Download Debian Container Template
Upload to Proxmox

1. Create LXC container
- Configure resources
  - CPU: 1 core
  - RAM: 2-4GB
  - Network: bridged to vmbr0
  - Assign static IP: 192.168.0.55

 2. Install Zabbix Repo
- `wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_7.0-1+debian12_all.deb
dpkg -i zabbix-release_7.0-1+debian12_all.deb`
- `apt update`


3. Install Zabbix Server and Components
- `apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent`

4. Import Zabbix Database Schema
- create database user Zabbix with password and import schema
- `zcat /usr/share/doc/zabbix-sql-scripts/mysql/create.sql.gz | mysql -u zabbix -p`

4a. Configure Zabbix Server
- edit config file to set DB password
- `sudo nano /etc/zabbix/zabbix_server.conf`
- # Set DBPassword=your_password

5. Start/Enable Services
- `sudo systemctl restart mariadb zabbix-server zabbix-agent apache2`
- `sudo systemctl enable mariadb zabbix-server zabbix-agent apache2`
- `systemctl restart zabbix-server zabbix-agent apache2`

 6. Access Zabbix Web UI
- navigate to http://192.168.0.55/zabbix
     

  




