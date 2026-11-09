
+++
author = "Alecks"
title = "Revised Homelab plans for 2026"
date = "2025-12-20"
description = "Changes I'll be making to my 2026 upgrade plan due to the surge in ram prices and various other computer parts like sourcing primarily second hand and just upgrading my existing hardware over building new machines."
tags = [
    "servers","homelab","self-hosting"
]
+++

Thanks to AI datacenters making the cost of RAM and Storage skyrocket, then making Micron one of the biggest manufacturers leave the consumer market (moving to exclusively serving these datacenters), the huge server cluster plans I had for 2026 really just aren't viable anymore. 

At the time each server would've cost around 2 and a half to 3 thousand aud, now just 128GB of DDR5 RAM [costs 3 thousand aud](/images/ddr5_ram_prices.webp) so I'll primarily use second hand hardware like mini pcs and legacy AM4 machines.

I will still be getting the job I mentioned in the previous 2026 homelab plans post, but the big ambitious plans I had for a full server rack just seem overkill and I wanted it more so I could show it off rather than practical use, most upgrades mentioned in this post are just adding new stuff to my existing machines.

### Current state of my setup
My original needs for a homelab are met, which was to cancel my vps and game server subscriptions, but now I need it to do a whole lot more. Replace my proton drive subscription (store backups of my computer files), host any future projects or apps I build, replace my icloud plus subscription (store photos using immich) and my crunchyroll subscription (maybe) with Jellyfin.

It consists of a custom built ryzen desktop and mini pc I got off ebay, both great computers and very efficient but I need more redundancy and better reliability before I trust it with more important data and critical services.

### Planned upgrades
A lot of these are centred around getting rid of my subscriptions, for data sovereignty, cost saving and media preservation reasons.
- **High-capacity storage**

To accommodate for my growing storage needs, I plan to attach at least two likely 4tb hdds in raid 1 (mirrored) and some small ssds as boot drives with plans for a proper ssd cache later on to my current ryzen box.

4tb seems like a safe future proof option for now that will fit my needs fine, I'm using raid 1 since its easy to setup but do want to experiment with something like zfs in the future.

This will be used for services that need lots of storage like my File Server (for backing up files on my computer), Immich and Jellyfin

- **Improved reliability and redundancy**

As I host *production* services such as live websites (like this one), game servers for communities and plan to use this setup for any future projects or apps I build everything runs in vms that can live migrate to other hosts if any machines need maintenance or cleaning (thanks to proxmox clustering).

Something I haven't resolved yet is keeping things online during power outages, most of the time caused by storms, a ups is an important investment I'll be making next year.

Hard drive redundancy with Raid or ZFS is definitely a high priority, right now there's offsite backups but if any drives fail onsite I'd need to buy a new drive and pull a backup from the cloud to get things back online, all nodes will be setup with dual nvme ssds setup in raid 1 (mirrored).

- **Local more in depth monitoring**

The addition of a Raspberry Pi running Grafana and Prometheus will give me a much more in depth monitoring system that's fully under my control and power efficient. 

I plan to use this as its a cheap low power machine thats seperate from the compute nodes, meaning if they both die it won't take my monitoring system with it.

### Concluding Thoughts

To recap everything that will be added next year
- 2x 4tb hdds in raid 1 that'll be attached to my ryzen box
- A UPS to protect against power outages primarily caused by storms 
- Redundant nvme storage on all machines
- Raspberry Pi as a dedicated monitoring server

Not entirely sure what I plan to do with networking right now, will discuss that later on in a future blog post, likely one dedicated to setting up my own custom opnsense router as that seems like a fun project I'll work on once these upgrades are finished.

Thanks for reading :)