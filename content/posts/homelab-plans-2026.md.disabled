
+++
author = "Alecks"
title = "Homelab Plan for 2026"
date = "2025-09-19"
description = ""
tags = [
    "servers","homelab","self-hosting"
]
+++

As great as my homelab is, there's still a ton of improvements I wanna make it to it for reliability, scalability and to learn new technologies, so lets go through them.

2026 is gonna be the year of upgrades, as I'll be employed making probably around 2k per month depending on how many hours I work.

## Moving to Rackmount Hardware
Not only would moving to a proper server rack (most likely [this one](https://www.amazon.com.au/VEVOR-Adjustable-Standing-Networking-Equipment/dp/B0C64YY7G7)) make it easier to add new compute nodes compared to the shelf all my hardware is currently on, it also looks way cooler.

To achieve this I'm gonna be moving from my Edgerouter 4 to a custom rackmount [opnsense](https://opnsense.org) router. As for compute nodes, I'll be moving Navi into a rackmount case.

I'll also be installing a patch panel so everything is nice and cable managed, with proper labeling to save future me a few all nighters.

## New Machines
Not only am I gonna be moving my existing node (Lightsail) into a [Silverstone RM23-502 Mini 2U](https://www.scorptec.com.au/product/cases/server-&-rackmount/97350-sst-rm23-502-mini) rackmount case to add to the rack and turning it into a VPS host node, I'm also gonna be adding a few new nodes to the cluster.
### VPS Host Node
As you probably read above, I'm gonna turn Lightsail into a dedicated node for hosting VPS servers for relability purposes (If I do any hardware changes on my personal machines other peoples stuff isn't affected) and to give my stuff more resources.
### New Primary Machine
My current primary node (Navi) has served me well but I need an upgrade for better performance and reliability (Such as implementing Raid 1, old motherboard only has 1 NVMe slot)

The hardware config is gonna look something like this
- CPU: Ryzen 7 7700
- Memory: 128/192GB DDR5 RAM (Depending on budget)
- Storage: Dual 2TB NVMe SSDs (Raid 1)
- Case: [Silverstone RM23-502 Mini 2U](https://www.scorptec.com.au/product/cases/server-&-rackmount/97350-sst-rm23-502-mini)
- Power Supply: Corsair RM850x

This machine is gonna be used to host linux labs, remote workspaces, game servers, hosting/mirroring my GitHub repos and packages, running my personal website and various other personal services.

### Storage Server 
My current onsite backup server (read more about that [here]()) is great but I want something with way more than 1TB of storage and some proper redundancy. It'll run a PBS VM (VM Backups) and Minio VM.

I'm not entirely sure what kind of hardware to get yet, but probably something not too powerful built for a good balance of efficiency and cost effectiveness
- CPU: Ryzen 5 7600
- Memory: 32GB DDR 
- Storage: a lot of high-capacity HDDs, not sure exactly how much yet
- Case: [Silverstone RM22-308](https://www.silverstonetek.com/en/product/info/server-nas/RM22-308/)
- Power Supply: Corsair RM850

-- --
Those are all the machines I have planned for right now, I've had ideas for a 3 node ceph cluster instead of the single storage server but It'll be way overkill for my needs and also a dedicated game server machine but that'll only be needed if my other services need more resources, which with the new primary compute node (an absolute beast) is highly unlikely.

## Network Upgrades
Since the NBN just released new 2 Gigabit plans the older maxxed out 1 Gigabit high upload plans (1000/400) just dropped in price by like $33 per month (On my ISP), currently my Internet is 1000/100 which means that big backups take *weeks* to upload, upgrading to 1000/400 would be a humungous noticeable improvement.

## Power Backups
Recently my power has been pretty unstable and a UPS has seemed more and more critical for smooth operations, with the migration to a server rack I will be installing a dual UPS system, heres a basic rundown
- UPS 1: Critical devices including the Router, NBN Box and Switch
- UPS 2: Compute nodes - VPS Host, Primary Machine & Storage Server

Seperating networking infrastructure from compute nodes means that nothing gets overloaded and is overall just good practice.

Both will be a Cyberpower rackmount UPS (Not sure exactly which model yet)

## Closing Thoughts
Upgrading my Homelab into a more sophisticated setup such as the one above might seem overkill but is essential for someone like me who uses it as their own "Digital Garden", it stores all my projects, personal notes, remote labs and much more so it must be as resilient and reliable as my budget allows.

I'm not sure what changes I'm gonna make after these as anything more than this is probably actually overkill and will make the power bill even higher, but we'll see what the future holds.