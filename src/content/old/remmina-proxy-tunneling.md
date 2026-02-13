---
title: 'Remmina + Proxy'
description: ''
pubDate: 'Dec 11 2025'
---

## Quick Reference

For the specific configuration the following setting has to be enabled: `Advanced > [X] Use system proxy settings` .  
After that remmina needs to be started like:
```
$> export https_proxy="socks5://127.0.0.1:[Port]" && remmina
```