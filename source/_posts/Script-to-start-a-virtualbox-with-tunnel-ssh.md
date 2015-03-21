title: "Script to start a virtualbox with tunnel SSH"
date: 2015-03-19 14:27:45
categories:
- Virtualbox
tags:
- Virtualbox
---
![Virtualbox](/thumbnails/virtualbox.jpg)

When you are not using Vagrant, you may need to start your machine by command line and instead of use port forward (some systems does not allow to forward port 80 for example), you can use Tunnel SSH.

To do so, you can use the script below:

```sh
#! /bin/sh

#killing the ssh tunnel ports
sudo kill -9 `ps -ef | grep ssh | grep -v grep | awk '{print $2}'`
rm -f socket-*

#Starting the machine
VBoxManage startvm YOUR_MACHINE_NAME --type headless

#Creating all tunnel SSH
sudo ssh -M -S socket-web -fnNT -L 80:localhost:80 root@10.10.5.15
sudo ssh -M -S socket-mysql -fnNT -L 3306:localhost:3306 root@10.10.5.15
sudo ssh -M -S socket-mongo -fnNT -L 27017:localhost:27017 root@10.10.5.15
sudo ssh -M -S socket-xdebug -fnNT -L 9000:localhost:9000 root@10.10.5.15
```