title: "Mounting shared folder on virtual box"
date: 2015-04-17 19:12:18
categories:
- Virtualbox
tags:
- Virtualbox
---
![Virtualbox](/thumbnails/virtualbox.jpg)

Sometimes is hard to understand each parameter of a command. I had to do a long research when I was trying to mount a folder inside of a virtual machine built with Virtualbox. The command needs a little explanation:

```sh
mount -t vboxsf <Name_of_the_share_config_on_virtual_box_application> <path_on_linux>
``

I tried this command several times, and nothing worked. So, I found the solution: **The Virtual box guest addon was not installed**.

```sh
apt-get install dkms
/etc/init.d/vboxadd setup
```

After that, I needed to discover that, the first param is the name inside of the Virtual Box application:

![Virtualbox](/images/Mounting-shared-folder-on-virtual-box.png)

Your command may looks like this:

```
mount -t vboxsf Sites /var/www
```

After that, everything worked for me.

If you want to mount with a specific owner (to avoid permission problem), you can do:

```
mount -t vboxsf -o uid=33,gid=33 Sites /var/www
```

Where 33 is the id of my www-data user.