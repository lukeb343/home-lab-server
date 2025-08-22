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
- this adds Zabbix's software source to my package manager so I can use `apt` to install it
- `wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_7.0-1+debian12_all.deb
dpkg -i zabbix-release_7.0-1+debian12_all.deb`
- `apt update`


3. Install Zabbix Server and Components
- installing all necessary componenets to run Zabbix
  - zabbix-server-sql: Core Zabbix server using MySQL/MariaDB
  - zabbix-frontend-php: Web UI
  - zabbix-apache-conf: Apache config
  - zabbix-sql-scripts: SQL schema to intitialize the zabbix database
- `apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent`
- These allow Zabbix to collect, store and monitor data


4. Import Zabbix Database Schema
- create database user Zabbix with password and import schema
- `zcat /usr/share/doc/zabbix-sql-scripts/mysql/create.sql.gz | mysql -u zabbix -p`
- Zabbix requires a specific database structure to function, this imports the reqauired tables and initial configuration for the DB


4a. Configure Zabbix Server
- edit config file to set DB password
- `sudo nano /etc/zabbix/zabbix_server.conf`
-  "Set DBPassword=your_password"
-  Without this password, the server can't communicate with teh database
-  NOTE: Even with password set earlier, I had to revist this conf.
  - Make sure line DBPassword is not written out with a # at the beginning


5. Start/Enable Services
- `sudo systemctl restart mariadb zabbix-server zabbix-agent apache2`
- `sudo systemctl enable mariadb zabbix-server zabbix-agent apache2`
- `systemctl restart zabbix-server zabbix-agent apache2`


 6. Access Zabbix Web UI
- navigate to http://192.168.0.55/zabbix



Fixes along the way:
-Resolved locale and PHP module issues.
-Imported clean Zabbix 7.0 database schema.
-Fixed DB version mismatches.
-Configured and secured DB user with password.
-Set up and secured Zabbix frontend.
-Enabled HTTPS using self-signed cert.
-Verified services and UI functioning properly.
     

  




