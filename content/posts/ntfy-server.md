+++
author = "Alecks"
title = "Setting up and securing a personal NTFY server"
date = "2025-09-06"
description = ""
tags = [
    "servers","self-hosting","ntfy","docker"
]
+++

[Ntfy](https://ntfy.sh) is an absolutely amazing service for sending push notifications to your phone or other devices with a simple web request, I use it for alerts from my uptime monitor (HetrixTools) and ssh logins. Mine is hosted on a google cloud free tier e2 micro instance which gives me great reliability for free.

Heres how to set it up with docker and proper authentication for personal use - you can find a guide on how to secure whatever Linux server your hosting this on [here](/posts/securing-server).

## Initial Setup
### Config File
Make a directory at /etc/ntfy then setup a config file
```
sudo mkdir /etc/ntfy
sudo nano /etc/ntfy/server.yml
```

Copy paste the text below into server.yml with the required changes
```
# General Config
base-url: "https://ntfy.example.com" # Change this to your URL
upstream-base-url: "https://ntfy.sh" # Required for notifications to work on iPhone

# Authentication
auth-file: "/var/lib/ntfy/user.db"
auth-default-access: "deny-all" # Block access to channels by default unless logged in
```



### User Database Creation
You have to manually create a user.db file in /var/lib/ntfy/user.db otherwise this won't work
```
sudo mkdir /var/lib/ntfy/
sudo touch /var/lib/ntfy/user.db
```
Then save that file with nothing in it

### Container Creation

Install Docker for your distribution
```
sudo apt install docker.io # (Ubuntu/Debian)
sudo dnf install docker # (Fedora/Red Hat)
```

Then run the command below which will
- Create a container for ntfy (named ntfy)
- Run it in the background (-d)
- Start at boot unless it was stopped (--restart=unless-stopped)
- Expose port 80 to 127.0.0.1:8080 so your reverse proxy can access it but its not exposed at your machines public IP
- Map directories for a cache and config file
```
sudo docker run \
-d \
-v /var/cache/ntfy:/var/cache/ntfy \
-v /etc/ntfy:/etc/ntfy \
-v /var/lib/ntfy:/var/lib/ntfy \
-p 127.0.0.1:8080:80 \
--name=ntfy \
--restart=unless-stopped \
binwiederhier/ntfy \
serve \
--cache-file /var/cache/ntfy/cache.db
```


## Reverse Proxy Configuration

Since its the best plug-and-play solution I'll be using [Caddy](https://caddyserver.com) for this guide, but there are several others, for example [Nginx](https://nginx.org)

Install Caddy and edit the Caddyfile
```
sudo apt install caddy -y
sudo nano /etc/caddy/Caddyfile
```
Then paste this config into it, replacing example.com with your actual domain of course
```
ntfy.example.com {
    reverse_proxy http://127.0.0.1:8080
}
```
Finally, restart your Caddy server
```
sudo systemctl restart caddy
```
Your ntfy instance should now be securely exposed!! Caddy will automatically fetch and install an SSL certificate for you

## Setting up Authentication

Only being able to access your server with an account was already configured in the initial setup process, now you just need to create an account to access it

Attach the ntfy containers shell
```
sudo docker exec -it ntfy /bin/sh
```

Then create a user account with the admin role
```
ntfy user add --role=admin example
```
It will then prompt you for a password, obviously change "example" to any username you want

Also, when sending notifications to channels most services want an access token, which you can create with this command
```
ntfy token add example
```

Hope this guide was helpful - for its creation I used several sections from the [ntfy docs](https://docs.ntfy.sh/) and a [networkchuck video](https://www.youtube.com/watch?v=poDIT2ruQ9M)