---
title: "Homelab"
author: "Alecks"
---

This setup hosts all of my core infrastructure which consists of several linux virtual machines and a couple lxc containers. Physical nodes run Proxmox VE (clustered)
### Compute Nodes

| Name | CPU | RAM | Storage |
| -------- | ------- | ------- | ------ |
| Lightsail | AMD Ryzen 5 5500 | 32GB DDR4 | 1TB SSD |
| Railway | Intel Core i5-7400T | 8GB DDR4  | 256GB SSD  |

### Additional Info
Both are connected to the Internet via a shared fibre line with gsl ddos protection, systems are monitored with hetrixtools (moving to on-prem prometheus soon).