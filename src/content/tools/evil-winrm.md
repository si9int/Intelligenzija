---
title: 'EvilWinRM'
description: ''
pubDate: 'Nov 28 2025'
target: 'win'
---

#### Installation

```
sudo apt install curl
gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
\curl -sSL https://get.rvm.io | bash -s stable
source /home/lux/.rvm/scripts/rvm
rvm pkg install openssl
rvm install ruby-3.4.7
gem install bundler
git clone https://github.com/Hackplayers/evil-winrm.git
cd evil-winrm && bundle add csv && bundle install --path vendor/bundle
```