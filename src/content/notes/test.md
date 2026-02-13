---
title: 'Google Dorking is not dead (yet)'
description: ''
pubDate: 'Feb 13 2026'
---

Somebody recently shared a link with me providing access to a cloud-based file service hosted by the Leibniz Supercomputing Centre (closely associated with the University of Munich). While the identifier itself appeared to be secure [\*], it was surprisingly easy to find other instances using a simple Google: `site:https://syncandshare.lrz.de/getlink/`. Some of the results exposing 'juicy' data.

A simple trick to anchor the dork is Google's 'Programmable Search Engine' (PSE). This not only refines the results but also simplifies automated processing ;-)

![PSE example](https://i.imgur.com/fV8oJIw.png)

---
[\*] With total length of 22-24 characters, a fixed `fi` prefix, and an encoding schema suggesting Base58/62, the search space consists of approximately 62^20 to 62^22 possible combinations (62 due to the alphanumeric base [a-z, A-Z, 0-9]). Example link: `/getlink/fiXYv4sBtHr2fvr7FtE2vF/`.