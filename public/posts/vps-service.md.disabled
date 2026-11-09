
+++
author = "Alecks"
title = 'How I host Linux VMs for people in my Homelab'
date = "2025-08-31"
description = ""
tags = [
    "linux","servers","homelab","vms"
]
+++
A lot of my Homelab typically sits idle, wasting power. So I had the idea of letting other people run their own linux virtual machines on it, kinda like how gcp offers "spot" vms for much cheaper as it uses excess compute capacity.

Obviously I can't provide this as a paid service since that comes with a lot of liability and legal documents to protect yourself, so I just offer it as a free service for friends.

## VM Templates & Operating Systems
I already use Proxmox VE for personal vms so I'm using my existing setup for this service.

Currently I have a vm template for Debian 13 "Trixie", which lets me spin up new machines with unattended updates and the setup process already complete.

## Networking & Public IPs
I had to get a bit creative here as residential internet connections don't let you have multiple public ip addresses on your connection.

To get around this I run a vps with multiple public ips which has a secure encrypted tunnel back into a tailscale gateway running inside my home network which exposes the vm subnets/network, this setup also means I don't have to install tailscale on any vms.

If someone connected to `[public_vps_ip]:22` it gets relayed to `[private_vm_ip]:22` through the tunnel and it all happens seemlessly.

![](/images/home_vps_diagram.webp)

This all happens behind the scenes without any noticeable latency (1-2ms latency between vps and my network, tailscale gateway gets under 0.2ms to vms)

## Internal Network Security
Obviously one of the main security risks with running a service like this in my Homelab isn't really external attacks, its vms being breached and then attacking or breaking into stuff on my home network.

To mitigate this I have a security group on the Proxmox firewall with a list of rules denying access to anything on my local network except the router (for internet) and tailscale gateway (to expose services). Running it on the hypervisor level adds an extra layer of security because you'd need access to Proxmox which is also firewalled off.

## Conclusion
This setup is still in the early stages of development, I've been working on it for a couple days so I'll improve over time as I make it more robust and reliable, one of my goals for later on is to add something like high availability or an automated system as most of it is manual right now.