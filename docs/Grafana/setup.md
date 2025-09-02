
Add grafana repo and install
apt-get install -y apt-transport-https software-properties-common wget gpg
Add grafana gpg key
wget -q -O - https://packages.grafana.com/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/grafana.gpg
Add grafana repo
echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
Enable and start grafana
‘Systemctl enable grafana-server’
‘Systemctl start grafana-server’

Issue: Checking grafana-server status it shows “Active: failed”
Checking logs shows
 grafana-server.service: Failed to set up …
grafana-server.service: Failed at step NAMESPACE
These namespace errors are because inside LXC containers systemd tries to apply sandboxing options that aren’t supported in containers
To fix, you need to override Grafanas systemd unit file and disable these restrictions
Create and override file
Systemctl edit grafana-server
Commented in 
[Service]
ProtectHome=false
ProtectSystem=false
PrivateTmp=false
NoNewPrivileges=false
ProtectKernelModules=false
ProtectKernelLogs=false
ProtectControlGroups=false
These didn’t work
** had to # comment out every single one of these
Grafana-server status is now Active: Running

Now access grafana web UI
Default login is
Admin
Admin


Installing Loki + promtail to feed Suricata logs into Grafana

In Grafana container: Install Loki
Update dependencies
apt update && apt install -y wget unzip
Create directories for Loki
mkdir -p /etc/loki /var/lib/loki
cd /etc/loki
Download loki binary
wget https://github.com/grafana/loki/releases/latest/download/loki-linux-amd64.zip
unzip loki-linux-amd64.zip
mv loki-linux-amd64 /usr/local/bin/loki
chmod +x /usr/local/bin/loki
Create a loki config
Pasted minimal loki config
Create systemd service
Took a while to get a config that it liked but finally got loki running


Installing Promtail: 
Downloading Promtail
cd /tmp
wget https://github.com/grafana/loki/releases/latest/download/promtail-linux-amd64.zip
unzip promtail-linux-amd64.zip
sudo mv promtail-linux-amd64 /usr/local/bin/promtail
sudo chmod +x /usr/local/bin/promtail
Create Directories
mkdir -p /etc/promtail
Create config: nano /etc/promtail/config.yml


server:
  http_listen_port: 9080
  grpc_listen_port: 0


positions:
  filename: /tmp/positions.yaml


clients:
  - url: http://localhost:3100/loki/api/v1/push


scrape_configs:
  - job_name: system
    static_configs:
      - targets:
          - localhost
        labels:
          job: varlogs
          __path__: /var/log/*log


Create systemd service: /etc/systemd/system/promtail.service


Start promtail
systemctl daemon-reload
systemctl enable promtail
systemctl start promtail
systemctl status promtail

