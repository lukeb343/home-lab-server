 Suricata IDS in Proxmox Homelab
Overview

This project explores building a network intrusion detection system (NIDS) inside a Proxmox homelab using Suricata.
The goal was to monitor LAN traffic, capture and analyze packets, and visualize the results with Grafana dashboards.

Architecture

Proxmox VE running on bare metal.

Suricata container with two NICs:

eth2 → management interface (assigned IP).

eth1 → monitoring interface (no IP, dedicated to packet capture).

Traffic mirroring configured on the Proxmox host to send LAN traffic into Suricata.

Loxi+ Promtail + Grafana for log collection, visualization, and alerting.

Achievements 

Deployed Suricata in a Proxmox container with dual interfaces.

Captured Layer 2 LAN traffic (ARP, STP, broadcasts) successfully.

Validated packet visibility with tcpdump, nslookup, and dig.

Integrated Suricata outputs into a Grafana dashboard for real-time monitoring and visualizations.

Lessons Learned 

Capturing traffic inside Proxmox requires careful NIC and bridge setup.

Without a managed switch or network TAP, visibility is limited primarily to L2 broadcasts.

Grafana integration provides strong insights even with partial traffic capture.

Next Steps 

Expand monitoring from L2 → full L3+ traffic (DNS, HTTP, TLS).

Add a dedicated TAP device or managed switch with port mirroring (SPAN).

Build detection/alerting rules for DNS tunneling, malicious domains, and HTTP anomalies.

Automate setup with Ansible or Terraform for reproducibility.



Skills Demonstrated 

Proxmox virtualization & container networking.

Suricata IDS deployment & configuration.

Linux networking tools (tcpdump, tc, ip link).

Log pipeline integration (Suricata → Grafana).

Hands-on troubleshooting with packet visibility.
