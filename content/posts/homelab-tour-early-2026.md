
+++
author = "Alecks"
title = "Homelab Tour (Early 2026)"
date = "2026-04-08"
description = ""
tags = [
    "servers","homelab","self-hosting"
]
+++

> The mid-2026 homelab tour is [now here](/posts/homelab-mid-2026/)!

## Introduction

Over these past few months of early 2026 my homelab has expanded to host many new game servers, proxy friends services and even run my own mini streaming service.

So I'll be taking you through everything behind the scenes that makes this possible, how I keep everything stable and my future expansion plans.

## Services

### Managed Game Hosting
I've had my game hosting platform for a while but only just recently has it become pretty active and filled to capacity, I actually had to upgrade the ram on one of my physical machines to accomodate for this demand. 

I have primarily modded minecraft, some paper/vanilla smps, ark and terraria all running inside docker containers managed by [pyrodactyl](https://pyrodactyl.dev) where users get their own account on my game panel to manage their servers console, files, network allocations and backups just like a proper hosting service.

The panel runs in its own vm and game servers also run in their own vm to stop the game servers or panel overloading and taking the other down.

### Jellyfin - streaming service

This is essentially my own self-hosted netflix, my friends with their own accounts can stream anything on demand from their phones, tvs, computers or anything that has a jellyfin client. 

Surprisingly this hasn't saturated my upload bandwidth yet even with multiple streams at once, as the service expands I might have to upgrade my internet.

### Proxying Friends Services

I've helped some new friends setup their own home servers using decommissioned computers I've gotten for free from my work experience place however both of them aren't able to port forward for different reasons so I run a proxy server at my place with game server ports forwarded to it which forwards traffic sent to those to my friends servers over a tailscale tunnel.

Their web services also proxied through my main caddy server using the same setup. This service allows my friends to bypass their port forwarding restrictions exposing their stuff through my network.


## Hardware

### Networking

My setup uses a small-business grade router and my servers are connected to an unmanaged gigabit switch, plan to upgrade eventually but for now 1 gigabit internal network is sufficient.

Since my ISP uses [GSL](https://globalsecurelayer.com) for IP transit I can get low latency to almost all other ISPs in my city.

### Compute Nodes - [Live Status](https://status.alecks.dev)

| Name | CPU | RAM | Storage |
| -------- | ------- | ------- | ------ |
| au-prox-01 | Ryzen 5 5500 | 64GB DDR4 | 1TB NVMe |
| au-prox-02 | Core i5-7400T | 16GB DDR4 | 256GB NVMe |

All servers run Proxmox VE clustered together which allows me to easily migrate vms and lxcs between machines if a server needs to be taken down for maintenance.

### UPS (Coming Soon)

Allows my systems to stay online during multi hour long power outages, I've already got one ordered and on the way its just gonna take a few weeks to arrive.

## Software

### Proxmox (Hypervisor)

This lets me contain all my services into their own "virtual" computers which lets me set super strict resource allocations on cpu, ram and storage and makes them portable so they're easy to move around and migrate between machines.

I also run a few lxcs for more lightweight services like my caddy gateway or tailscale subnet router.

On au-prox-01 I have an Ubuntu Server template with cloud-initd which I clone and configure to setup new vms without having to spend ages waiting for a linux install.

### Docker (Containers)
Runs on my service vms and contains everything into their own containers and bundles dependencies making it super easy to deploy things. It's heavily integrated with my game panel and I use it outside of that to run pretty much everything like jellyfin, grafana, prometheus, node exporters and more.

Not the best explanation if you're interested I'd recommend looking at one of the hundreds of guides or videos online talking about it.

### Prometheus & Grafana (Local Monitoring)

This collects detailed metrics about my servers resource usage, temperature and more running on a dedicated monitoring vm in my proxmox cluster, I plan to move it to its own machine soon but its not a priority currently when its more of a backup for if my internet goes down and hetrixtools can't recieve metrics.

## Third Party Services

### HetrixTools & NTFY (External Monitoring)

All my servers and vms have heartbeat monitors on them so they run an agent that sends data to the hetrixtools every minute and if it doesn't send anything for more than 5 minutes its marked as offline, this collects cpu, memory, storage, disk health, network traffic and system info.

My [public status page](https://status.alecks.dev) uses this service for its metrics.

NTFY is a mobile push notification service I'm hosting on a vps (hetrix is cloud based and not self-hostable), its connected to hetrix so if a server goes offline or for example the cpu is getting hammered I get an alert on my phone.

### Cloudflare R2 (Offsite Backups)

An s3-compatible storage service I send backups to, not really much to say about this except that its not super expensive, reliable and has worked pretty well so far but may get pricy when I expand my storage locally.

## Future Plans

- Migrating to a server rack instead of just having everything on a shelf
- A local backup server so restores are super quick and to stay compliant with the 3-2-1 rule.

## Conclusion

This homelab is mostly sufficient for my needs right now but as I continue to expand theres still a lot I want to do and add for quality of life, looks and reliability.

Thanks for reading :)