---
title: 'Enable Folder Sharing in QEMU/KVM'
description: ''
pubDate: 'Nov 30 2025'
---

## Requirements

```
$h> sudo apt update
$h> sudo apt install virtiofsd
```
Next open "virt-manager" and enable shared memory within the VM by navigating to `Memory > [X] Enable Shared Memory` . After rebooting the VM a shared filesystem can be added. This can be done by adding new hardware ("Add Hardware") and choosing "Filesystem" with the following details: 

- Driver: virtiofs
- Source path: [folder on host]
- Target path: [unique identifier e.g. shared_from_host]

After submission, restart the VM and mount the new share.

## Mount Permanently

```
$g> mkdir ~/shared
$g> sudo nano /etc/fstab
...
[identifier] /home/[username]/shared virtiofs defaults 0 0
...
$g> sudo mount -a
```

## Mount Temorarily

```
$g> sudo mount -t virtiofs [identifier] ~/shared
```