---
title: 'Mirror Traffic from Guest to Host'
description: ''
pubDate: 'Dec 02 2025'
---

## Scenario

A VPN-connection utilisied within a VM needs to be bridged over to the host, so that the host can access the associated network(s) (e.g. via a web browser).

## Solution: SOCKS5 (SSH Tunnel)

```
$h> ssh -D 1337 -f -C -q -n [username]@[IP]

# -D = creates a [D]ynamic SOCKS proxy on local port 1337
# -f = runs SSH in the background ([f]arewell)
# -C = enables data [C]ompression
# -q = enables [q]uiet mode
# -n = prevents reading from STDIN (handy in combination with -f)
```

The tunnel can then be used as a SOCKS5-proxy running on: `127.0.0.1:1337` .
