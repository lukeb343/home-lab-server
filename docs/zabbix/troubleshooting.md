# Zabbix Installation and Troubleshooting Notes

## Problem: Broken Packages on Ubuntu
- **Error:** `Unable to correct problems, you have held broken packages.`
- **Cause:** Missing dependencies not included with Ubuntu.
- **Steps Taken:**
  - Attempted installation on Ubuntu but required packages were unavailable.
- **Solution:** Installed Debian instead, which includes the necessary dependencies and works out-of-the-box with Zabbix.

---

## Problem: "System Locale = Fail" on Zabbix Pre-requisite Check
- **Issue:** All locales were set to `=C` and showing LC errors.
- **Steps Taken:**
  1. Verified Zabbix components:
     - `systemctl status zabbix-server` → active
     - `systemctl status zabbix-agent` → active
     - `systemctl status apache2` → active
     - `systemctl status php-fpm` → not found
  2. Checked if php-fpm was installed:
     - `dpkg -l | grep php | grep fpm` → blank (not installed)  
     - Installed `php8.2-fpm` and started service → confirmed active.
  3. Checked system locales:
     - `locale -a` → `en_US.UTF-8` missing.
     - Ran `locale-gen en_US.UTF-8` (partial fix, still showing `=C`).
  4. Edited `/etc/default/locale` to set:
     ```bash
     LANG="en_US.UTF-8"
     LC_ALL="en_US.UTF-8"
     ```
     (This fixed most values but not all.)
  5. Ran `dpkg-reconfigure locales` and selected `en_US.UTF-8`.  
     - Fully installed and fixed locale issues.
- **Solution:** Install and configure `en_US.UTF-8` properly as the system default locale.

---

## Problem: "Unable to determine current Zabbix database version: dbversion table not found"
- **Issue:** No schema file was found in the expected location.
- **Steps Taken:**
  1. Manually downloaded schema files:
     ```bash
     wget https://cdn.zabbix.com/zabbix/sources/stable/7.0/zabbix-7.0.3.tar.gz
     tar -xvzf zabbix-7.0.3.tar.gz
     cd zabbix-7.0.3/database/mysql
     ```
  2. Created a new Zabbix database and imported schema.
- **Solution:** import schema manually into the database to resolve missing `dbversion` table.

 ---

## Problem: Zabbix Dashboard shows "Zabbix Server is not running"
- **Issue:** Service was active, but dashboard reported it wasn’t.
- **Steps Taken:**
  1. Checked `/etc/zabbix/zabbix_server.conf`.
  2. Found `DBPassword` line was commented out.
  3. Removed `#` before:
     ```bash
     DBPassword=mypassword
     ```
---

- **Solution:** Uncommented `DBPassword` line to allow proper server connection.
## Problem (8/24/2025): Cannot login to Zabbix Web UI
- **Error:**  "you are not logged in" Possibly the session has expired or password was changed.

- **Steps Taken**
1. Checked system time with `date` → host time correct, Zabbix set to UTC.
2. Confirmed login worked in incognito tab → indicated browser cookie/session issue.
- **Solution:** Cleared cookies and site data, which resolved login issue.
