---
title: 'Enable Folder Sharing in QEMU/KVM'
description: ''
pubDate: 'Nov 30 2025'
---

##### Requirements

```
sudo apt update
sudo apt install virtiofsd (host)
```

Then open e.g. "virt-manager" and configure the VM by navigating to "Memory", checking "Enable Shared Memory" and apply.
Next add a shared filesystem using "Add Hardware" choosing "Filesystem" (Driver: "virtiofs", Source path: folder on machine, Target path: !identifier! [e.g. shared_from_host]). Start VM!

##### Mounting

```
mkdir ~/shared
sudo nano /etc/fstab
[identifier] /home/[username]/shared virtiofs defaults 0 0
sudo mount -a
```

##### Mount Temorarily

```
sudo mount -t virtiofs [identifier] ~/shared
```