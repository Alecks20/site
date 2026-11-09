
+++
author = "Alecks"
title = "Securing ssh on your Linux Server"
date = "2024-04-25"
description = ""
tags = [
    "linux","servers","ssh","security"
]
+++

This post is made for debian based linux distros.

### Don't expose ssh, use a VPN
This is obviously not viable for stuff running in the cloud but for a homelab server its advised to not expose ssh or management ports, if you need external access use a VPN service like Tailscale or self-hosted Wireguard.

### Non-root account for logins / Disable root login
Disabling the ability to login as root helps with many automated bots that brute-force ssh into your server, start by making a new user with any username you want

```
adduser kuma
```

Then add it to the list of sudoers

```
usermod -aG sudo kuma
```

### Using SSH keys over plaintext passwords
SSH Keys are both more convenient and more secure than a regular plaintext password, especially the default one set by your hosting provider. 

Generate an ssh key using PuttyGen and paste it on a new line in `/home/<your_username>/.ssh/authorized_keys`.

### Updating your SSH configuration
This process can differ depending on your host, but for most servers the ssh config is located in `/etc/ssh/sshd_config`, in the file you want to change the following values.

```
PasswordAuthentication no
```

```
PubkeyAuthentication yes
```

```
PermitRootLogin no
```

Changing these config values will
- Disable password authentication
- Allow you to login using ssh keys (Which I showed how to setup above) 
- Disable root login (Applying the steps from before)

Run the command below to apply the motifications

```
sudo systemctl restart ssh
```

### NTFY notifcations on ssh login
You can learn how to setup a secure personal ntfy server [here](/posts/ntfy-server).

Adding these lines to your `/etc/profile` file will send a request to your chosen ntfy server when any user logs in via ssh

```
if [ -n "$SSH_CLIENT" ]; then

NTFY="${USER}@$(hostname -f) from $(echo $SSH_CLIENT|awk '{print $1}')"

curl -u :<ntfy_api_key> -s -H "Title: SSH Login" -d "$NTFY" -L  "https://ntfy.exaple.com/ssh" > /dev/null

fi
```
Modify to add your own api key and change the url to your ntfy server


You can also find an example on the ntfy docs [here](https://docs.ntfy.sh/examples/#ssh-login-alerts) (Didn't work for me)