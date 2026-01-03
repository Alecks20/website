---
title: "Homelab"
---

This setup hosts all of my core infrastructure which consists of several Linux VMs and a couple LXC Containers. VM nodes run Proxmox VE (Clustered).

The VMs themself run various different services including remote workspaces, self-hosted applications, game servers and this website, some offsite services are utilized to expose everything to the internet.
### Compute Nodes - [Live Status](https://status.alecks.cloud)

| Name | CPU | RAM | Storage |
| -------- | ------- | ------- | ------ |
| au-prox-01 | Ryzen 5 5500 | 32GB DDR4 | 1TB NVMe |
| au-prox-02 | Core i5-7400T | 8GB DDR4 | 256GB NVMe |

Some upgrades to existing machines are coming soon.
### Backups & Monitoring
- ~~Daily backups of vm disks are sent to my local PBS server (incremental), then mirrored onto Hetzner object storage and stored for 7 days.~~ Currently no vm level backup system, game nodes run their own daily backups of server volumes.
- [HetrixTools](https://hetrixtools.com) monitors server resources (cpu, ram, storage and bandwidth usage), uptime, drive health, detects outages and pushes alerts to my ntfy server.
- Additionally, I have an on-prem prometheus and grafana setup which extensively monitors all vms.
- [ntfy](https://ntfy.sh) notifies me of incidents picked up my hetrix with mobile push notifications.

### Reliability
- Power outages happen at max a couple times a year and everything is designed to automatically recover when systems come back online (UPS backup will be installed soon to mitigate that).
- Internet has never gone down before, my router is reliable and semi-enterprise grade.
