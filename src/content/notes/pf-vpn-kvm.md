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

drop -p and --dport/sport = all protocols accepted

sudo iptables -I LIBVIRT_FWO 1 -i virbr0 -o tun0 -s 192.168.X -j ACCEPT
```

Check with:

```
sudo iptables -L LIBVIRT_FWI -n -v
sudo iptables -L LIBVIRT_FWO -n -v
sudo tcpdump -i any port 389
sudo nc -nlvp 389 (Guest)
echo "hi" | nc 192.168.X.X 389 (Host)
```

---

#### Creating a local bridge

```
sudo ip link add br0 type bridge
sudo ip addr add 192.168.50.1/24 dev br0
sudo ip link set br0 up
(host)
```

```
QEMU > add hardware > network > XML
<interface type='bridge'>
  <source bridge='br0'/>
  <model type='virtio'/>
</interface>
```

```
sudo ip addr add 192.168.50.2/24 dev eth1
sudo ip link set eth1 up
(guest)
```

```
sudo iptables -t mangle -A PREROUTING  -i tun0 -j TEE --gateway 192.168.50.2
sudo iptables -t mangle -A POSTROUTING -o tun0 -j TEE --gateway 192.168.50.2
(mirror VPN traffic via TEE)
```

```
sudo iptables -t mangle -L PREROUTING -v -n
sudo iptables -t mangle -L POSTROUTING -v -n
sudo tcpdump -i eth1
(debugging)
```