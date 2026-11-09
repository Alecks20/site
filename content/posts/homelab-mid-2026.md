
+++
author = "Alecks"
title = "Homelab Tour (Mid 2026)"
date = "2026-07-01"
description = ""
tags = [
    "servers","homelab","self-hosting"
]
+++

To start with the mid 2026 homelab tour, some very significant changes have happened that've completely elevated the setup onto another level.
- The installation of my new 1600VA pure sinewave ups, this has already kept my homelab online during late night 30-40 minute power outages.
- Moving to a server rack and rackmount hardware, this has made the setup look much more refined and helped a lot with organisation
- New full size server, au-prox-03 which is built using parts ganked out of a hp prodesk and ssd from a laptop put with a new motherboard, casing and psu.
- Moved au-prox-02 onto a new i5 10th gen nuc and am now using the i5 7th gen mini pc as a proxmox backup server.

This post will consist of changes since the [last post](/posts/homelab-tour-early-2026/), anything not mentioned here has been kept the same.

## UPS / Battery Backup
Back in April I ordered a [CyberPower 1600VA UPS](https://www.amazon.com.au/dp/B0DCZFCFRS?ref=ppx_yo2ov_dt_b_fed_asin_title) for $470 AUD, since then its been installed and held up very well powering all my networking gear and servers, keeping the entire rack online and accessible during outages, power trips and protecting psus against rare brownouts and fluctuations.

On average I'm pulling around 150-200W with everything running, at full load It'll pull 250w+. With the UPS capacity at about 1000W it can easily keep everything on for over half an hour which clears short outages and power trips.

For longer outages I have NUT configured on my proxmox hosts to shutdown as soon as the battery starts getting low to ensure everything shuts down correctly.

## Moving to rackmount hardware
The entire setup now operates out of a 15U server rack I picked up off amazon, it has a patch panel, rackmount power strip and the original au-prox-01 built 2 years ago got case swapped from the thermaltake tower case into a new [silverstone rm23-502 mini 2u](https://www.scorptec.com.au/product/cases/server-rackmount/97350-sst-rm23-502-mini) (kinda hard to find in stock now for some reason) with noctua fans and cpu cooler.

## New hardware

The au-prox-02 node has been migrated off the lenovo i5 7th gen mini pc to a i5 10th gen intel nuc, with the old lenovo mini pc now setup as a proxmox backup server (au-bak-01)

I've also added a new rackmount server au-prox-03 rocking an i7-8700 16gb ddr4, 256gb nvme boot drive plus 2 2tb hdds setup in raid 1. This runs my nas vm (zimaos), matrix server and anything I access locally, It's also just extra capacity or spare compute if I need to take a vm host down temporarily.

The cpu and ram in au-prox-03 is salvaged out of a hp prodesk, the ssd is from an old laptop (obviously I've run smart tests on it and the virtual disks on it get backed up). Everything else like the motherboard, power supply, cpu cooler, fans and case are all brand new or certified refurbished off ebay.

## VM disk backups

To protect against host boot disk failures, I've setup the old au-prox-02 machine as a proxmox backup server with 500gb of nvme storage storing incremental daily backups of virtual machine disks, with plans to setup offsite syncing either with the cloud or a friends place later on.


## Concluding thoughts
The main focus with these upgrades has been making the setup more fit for hosting production services and stuff people depend on, I feel like I've achieved that and at a level now where I can host stuff without stressing about things like disk failure, power outages, brownouts etc.

Other that whats been mentioned in the post most of the software and services side has stayed pretty much identical if you don't include my nas now storing computer backups and my photos with immich.

What I wanna do in the future is 
-  Expand the cluster with more servers.
- Get redundant internet lines, business internet and more upload bandwidth.
- Eventually buy an even bigger higher quality rack and upgrade the networking gear to either a custom opnsense setup, mikrotik or unifi.
- Build a GPU server for running local AI models with openwebui or openclaw.

Thanks for reading :)