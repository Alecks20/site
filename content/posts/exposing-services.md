+++
author = "Alecks"
title = "Exposing self-hosted applications without a Public IP address"
date = "2025-08-30"
description = ""
tags = [
    "servers","homelab","self-hosting"
]
+++

In a perfect world everyone could port forward and use an ISP with DDoS Protection and Static IPs, however we don't live in a perfect world. Many people have to deal with things like CGNAT (no public ip) and annoying ISPs.

So here are a few **free and paid** solutions for exposing both web applications and game servers to the internet without port forwarding.

## [Cloudflare Tunnels](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/)
This is a completely free service which supports exposing only web applications to the internet using an application (cloudflared) running on your server which tunnels traffic out and exposes it via the Cloudflare Network

Some argue that it defeats the point of self-hosting since Cloudflare centralizes the web while the indie webs goal is the opposite, however its a great service for exposing applications for free if your fine with that tradeoff.

## [Tailscale](https://tailscale.com) (w/ an optional VPS)

This solution can be either free or paid depending on if you want just yourself to be able to access your services or you want them to be exposed via a domain. You can setup Tailscale on both your devices and the server then securely connect to eachother without exposing anything publicly for completely free.

If you want a service to be publicly accessible via a domain, you'll need a remote server with its own public ip address as Tailscale only lets you establish secure connections between devices, not expose things to the internet.

You'd install Tailscale on your home server and remote server, then on the remote server you install for example caddy and setup a reverse proxy to your home servers Tailscale address, an example config is shown below.
```
example.com {
  reverse_proxy http://100.85.48.32
}
```

Additionally, you can use this to expose any tcp/udp service, including Game Servers, SSH, (S)FTP and much more which requires forwarding ports from a remote server to your home servers Tailscale address but I don't feel confident explaining how to do that.

## [Playit.gg](https://playit.gg)

Arguably the best free service for exposing game servers without port forwarding. The setup includes installing a program which tunnels game server traffic to their global network of relay servers.

Its super easy to setup, you can watch a video guide [here](https://www.youtube.com/watch?v=itVVhcid2_Q&pp=ygUUc2V0dGluZyB1cCBwbGF5aXQuZ2fSBwkJsgkBhyohjO8%3D).

You can also use it to expose any tcp port with a dedicated IPV4 but Tailscale w/ a VPS or CF Tunnels (for websites) is a better option since playit is primarily for game servers.