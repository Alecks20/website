+++
author = "Alecks"
title = "Moving to Prometheus and deploying a k3s cluster"
date = "2026-01-03"
description = "Going over some major changes to my monitoring system and addition of a new kubernetes cluster, which isn't yet ready for production."
tags = [
    "servers","self-hosting","k3s","prometheus","monitoring"
]
+++

I've been watching a lot of homelabbing content recently and decided to setup some new services specifically for improving reliability, observability and adding new functionality.

Both of these I just got started with yesterday so my knowledge is quite limited, I intend to slowly improve these setups overtime.

## Prometheus and Grafana / On-prem monitoring
I wanted a flexible self-hosted solution that didn't run in the cloud while being able to monitor proxmox nodes, vms and more sophisticated monitoring with specific services like databases or kubernetes clusters which hetrixtools can't do, so I ended up on prometheus and grafana.

I'm running it on a dedicated monitoring vm running them both in docker, to access it remotely I use tailscale and I run node exporter on all my vms then pull that data here over local network or the internet (for vpses) with proper firewalling.

In the future I plan to put this system on its own seperate hardware like a raspberry pi not in the proxmox cluster so that if theres failures this system doesn't go down with it.

![](/images/grafana.webp)

<sup>Slightly modified version of the [node exporter](https://grafana.com/grafana/dashboards/1860-node-exporter-full/) dashboard</sup>

It's currently using just premade templates which are very complex and sophisticated but I plan to make my own custom dashboards in the future as I monitor more, shoutout to [this article](https://dellavedaffa.medium.com/run-node-exporter-as-a-background-service-in-5-minutes-with-python-systemd-a58a51c42672) for helping me setup node exporter on machines that I don't have docker on (like proxmox nodes)

I use this command to deploy the node exporter via docker on my machines.

```
docker run -d \
  --name=node_exporter \
  --restart=always \
  --net="host" \
  --pid="host" \
  -v "/:/host:ro,rslave" \
  prom/node-exporter:latest \
  --path.rootfs=/host
```

## K3s Cluster
I've taken an interest in something called "mini labbing" where people use things like raspberry pis or mini pcs (e.g second hand lenovo thinkcentres), put them in a mini rack and use them as a homelab, additionally one of my favourite productivity youtubers jvscholz [made a video on homelabbing](https://www.youtube.com/watch?v=bKC2M34iKtw) where he mentioned making a kubernetes cluster.

On top of that I've seen kubernetes being used a lot in production enterprise deployments and stuff like that so I thought learning it must be pretty a importmant skill, so why not start now.

![](/images/kubernetes_dashboard.webp)

As you can see I have 3 k3s nodes setup, node 1 is the "control plane" and worker node running the dashboard and the other ones are just worker nodes.

I used the [k3s install guide](https://docs.k3s.io/installation) to install it and [this]() guide to setup the dashboard. They're currently just vms on top of proxmox as its more of a lab/testing environment for learing kubernetes rather than an actual production environment, had a lot of fun with it so far.

## Closing Thoughts
These have been very fun to learn and setup, even more excited to see what I'm able to do with these in the future like running production apps in kubernetes hosted on multiple physical machines instead of vms possibly even mini pcs.

Thanks for reading :)