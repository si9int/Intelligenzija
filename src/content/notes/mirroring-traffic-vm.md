---
title: 'Traffic Mirroring: VM to Host'
description: ''
pubDate: 'Dec 02 2025'
---

#### Situation

We have virtual machine (VM) which runs a VPN-tunnel within the VM (no host access).<br>
The objective is to access the VPN-traffic *outside* the guest (e.g. via web browser on the host system).

```
# create a SSH tunnel
# -D = creates a [D]ynamic SOCKS proxy on local port 1337
# -f = runs SSH in the background ([f]arewell)
# -C = data [C]ompression
# -q = [q]uiet mode
# -n = prevents reading from STDIN (useful in combination with -f)

$> ssh -D 1337 -f -C -q -n [username]@[ip]
---
# create a second SSH session and start the VPN
# -s = [s]ession-name
# -d = starts session [d]etached (in the background)

$> tmux new-session -s vpn -d 'openvpn ~/connect.ovpn'
```


The tunnel can be accessed on the host as a SOCKS5-proxy: `[ip]:1337` .