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
- 'wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_7.0-1+debian12_all.deb
dpkg -i zabbix-release_7.0-1+debian12_all.deb' (Installs Zabbix Repo)
-apt update

3. Install Zabbix Server and Components
- `apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent`




