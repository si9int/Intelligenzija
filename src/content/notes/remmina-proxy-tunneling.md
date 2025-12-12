---
title: 'Remmina Proxy Tunneling'
description: ''
pubDate: 'Dec 11 2025'
---

**Requirement:** check `Advanced / [x] Use system proxy settings` for the specific configuration file via the Remmina GUI.  
Note: only compatible for version >= 1.4.31
```
$> export https_proxy="socks5://127.0.0.1:[Port]"
$> remmina
```