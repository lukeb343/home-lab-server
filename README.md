# Homelab Setup

This repository documents my personal homelab environment — a space where I test, learn, and experiment with various technologies, tools, and infrastructure setups. It serves as both a portfolio and a knowledge base for projects I’ve built or am currently working on.

## Goals
- Build hands-on experience with IT infrastructure and DevOps tools.
- Automate deployments and practice Infrastructure-as-Code (IaC).
- Explore self-hosted services and system administration.
- Learn networking, virtualization, and security concepts in a practical way.

## Hardware Overview

**Host Machine Specs:**
- **CPU:** Intel i5-4460 
- **RAM:** 16GB DDR3
- **GPU:** GTX 950
- **Storage:** 128GB SATA SSD, 2x 4TB WD RED, 1TB WD Blue
- **Network:** Gigabit Ethernet

---

##  Host OS & Hypervisor

I use **Proxmox VE** installed directly on bare metal. It provides a clean, web-based interface to manage all virtual machines, containers, and storage.

- Installed directly on the main desktop
- Managed through Proxmox web GUI

---

## Services
Some of the key services running in my homelab:

- Virtualization/Containerization: Proxmox, LXC containers, 
- Infrastructure Management: None currently, looking to incorporate Anisible
- Monitoring & Logging: Zabbix, Grafana*
- Networking/Security: Pi-hole
- Self-Hosted Services: TrueNAS

Looking to add, pfSense, Grafana, Wireguard, incorporating Anisible/or Terraform

---

##  Storage Setup (TrueNAS)

**TrueNAS** is deployed as a virtual machine within Proxmox, functioning as a NAS for managing file storage, SMB shares, and future ZFS experiments.

- **TrueNAS Scale**
- Passed-through storage disks from Proxmox to TrueNAS VM
- Configured redundant storage
- SMB shares for LAN access

---

## Virtual Machines

| VM Name       | OS            | Purpose                     | Access Method        |
|---------------|---------------|-----------------------------|----------------------|
| `truenas`     | TrueNAS Scale | File storage and sharing    | CLI/Web UI           |
| `Windows 2025`| WinServer 2025| Domain Controller           | RDP from main PC     |
| `Win11`       | Windows 11 Pro| Test Enviroment/ domain join| SSH / Web UI         |



---
## Repo Stucture
/docs # notes, setup guides, troubleshooting, screenshots
/
## Purpose

This homelab serves as a personal learning environment for:
- Virtualization and storage management
- Networking and remote access
- OS testing and scripting
- Experimenting with self-hosted services

---

