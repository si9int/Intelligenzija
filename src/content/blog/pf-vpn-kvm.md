---
title: 'Port Forwarding VPN to KVM/QEMU'
description: ''
pubDate: 'Nov 28 2025'
---

#### iptables magic

```
sysctl net.ipv4.ip_forward
sudo iptables -t nat -A PREROUTING -i tun0 -p tcp --dport 389 \
  -j DNAT --to-destination 192.168.X:389
sudo iptables -I LIBVIRT_FWI 1 -i tun0 -o virbr0 -d 192.168.X -p tcp --dport 389 -j ACCEPT
sudo iptables -I LIBVIRT_FWO 1 -i virbr0 -o tun0 -s 192.168.X -p tcp --sport 389 -j ACCEPT
```

Check with:

```
iptables -L LIBVIRT_FWI -n -v
iptables -L LIBVIRT_FWO -n -v
tcpdump -i any port 389
nc -nlvp 389 (Guest)
echo "hi" | nc 192.168.X.X 389 (Host)
```