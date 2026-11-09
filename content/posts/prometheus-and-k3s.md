+++
author = "Alecks"
title = "Moving to Prometheus and deploying a k3s cluster"
date = "2026-01-03"
description = ""
tags = [
    "servers","self-hosting","k3s","prometheus","monitoring"
]
+++

I've been watching a lot of homelabbing content recently and decided to setup some new services specifically for improving reliability, observability and adding new functionality.

My knowledge is quite limited currently as I'm just getting started, I intend to slowly improve these setups overtime.

## Prometheus and Grafana / On-prem monitoring
To prevent me from having no insignt into my homelab during an internet outage, I needed a monitoring solution that runs locally and stores everything locally, not on someone elses server. So I landed on prometheus as the monitoring service hooked up to grafana to visualize the data all running in docker.

I'm running them on a dedicated monitoring vm in docker containers, to access it remotely I use tailscale and run node exporter on all my vms then pull that data here over local network, the internet (for vpses) with proper firewalling or tailscale for servers hosted at friends houses.

In the future I plan to put this system on its own seperate hardware so that its seperate from my proxmox cluster if that fails or has quorum issues.

It's currently using just premade templates which are very complex and sophisticated but I plan to make my own custom dashboards in the future as I monitor more, hetrixtools is my primarily monitoring solution hooked up to my ntfy server for mobile alerts for downtime and resource usage, this is like a backup system to collect more detailed metrics and offer a safety net if my internet dies or anything happens to my hetrixtools account I still have a huge metrics collection stored locally.

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

On top of that I've seen kubernetes being used a lot in production enterprise deployments and stuff like that and I thought learning it must be pretty a importmant skill, so why not start now.

![](/images/kubernetes_dashboard.webp)

As you can see I have 3 k3s nodes setup, node 1 is the "control plane" and worker node running the dashboard and the other ones are just worker nodes.

I used the [k3s install guide](https://docs.k3s.io/installation) to install it and [this]() guide to setup the dashboard. They're currently just vms on top of proxmox as its more of a lab/testing environment for learing kubernetes rather than an actual production environment, had a lot of fun with it so far.

Have some ideas in the future like 

## Closing Thoughts
These have been very fun to learn and setup, even more excited to see what I'm able to do with these in the future like running production apps in kubernetes hosted on multiple physical machines instead of vms possibly even mini pcs.

Thanks for reading :)