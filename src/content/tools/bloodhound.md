---
title: 'BloodHound'
description: ''
pubDate: 'Nov 28 2025'
version: 8.4.1
target: 'win'
---

## Requirements

```
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF
sudo apt update
wget https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb
sudo dpkg -i docker-desktop-amd64.deb | sudo apt --fix-broken install
# optional: get a car from bavaria

```

## Installation

```
wget https://github.com/SpecterOps/bloodhound-cli/releases/latest/download/bloodhound-cli-linux-amd64.tar.gz
tar -xvzf bloodhound-cli-linux-amd64.tar.gz
./bloodhound-cli install
```

## Password Reset

``` 
./bloodhound-cli resetpwd
```