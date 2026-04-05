---
title: "Homelab"
---

This setup hosts all of my core infrastructure which consists of several Linux VMs and a couple LXC Containers. VM nodes run Proxmox VE (Clustered).

The VMs themself run various different services including game servers for me and my friends, aquaintances or small communities, a small jellyfin instance, matrix, websites and also acts as a gateway for my friends homelabs using tailscale.
### Compute Nodes - [Live Status](https://status.alecks.dev)

| Name | CPU | RAM | Storage |
| -------- | ------- | ------- | ------ |
| au-prox-01 | Ryzen 5 5500 | 64GB DDR4 | 1TB NVMe |
| au-prox-02 | Core i5-7400T | 8GB DDR4 | 256GB NVMe SSD |
| au-prox-03 | Core i7-7700 | 16GB DDR4 | 256GB NVMe SSD |

(Anything on the status page not shown above is either a vm or vps)
### Backups & Monitoring
- ~~Daily backups of vm disks are sent to my local PBS server (incremental), then mirrored onto Hetzner object storage and stored for 7 days.~~ Currently no vm level backup system, game nodes run their own daily backups of server volumes. I do have plans to setup an offsite backup server at one of my friends houses.
- [HetrixTools](https://hetrixtools.com) monitors server resources (cpu, ram, storage and bandwidth usage), uptime, drive health, detects outages and pushes alerts to my ntfy server.
- Prometheus and Grafana extensively monitors vms, vpses and vm hosts and acts as a backup to HetrixTools, since its hosted on-prem it still collects metrics if my internet ever went down.
- [ntfy](https://ntfy.sh) notifies me of incidents picked up my hetrix with mobile push notifications, hosted on a cloud server so if my entire homelab goes offline I can still get nofified.
- [Tailscale](https://tailscale.com) lets me access any vm or vm host running internally from outside my network without me needing to expose any ssh ports or run an ssh gateway.

### Reliability
- Power outages happen at max a couple times a year and everything is designed to automatically recover when systems come back online (UPS backup will be installed soon to mitigate that).
- Internet has never gone down before, my router is reliable and been rock solid under load.
