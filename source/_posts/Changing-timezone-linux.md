title: "Changing timezone linux"
date: 2015-03-19 14:27:59
categories:
- Linux
tags:
- Linux
---
![Linux](/thumbnails/linux.jpg)

Sometimes you need to change your linux machine date/time and a simple date function does not work. To change the timezone, you should edit your timezone file, change to your timezone area and then, run a command to validate it.

```sh
vim /etc/timezone
#Insert your timezone: e.g. America/Sao_Paulo

dpkg-reconfigure --frontend noninteractive tzdata
```

Source:
[http://odesenvolvedor.andafter.org/publicacoes/alterando-a-timezone-do-ubuntu-pelo-terminal-2.html](http://odesenvolvedor.andafter.org/publicacoes/alterando-a-timezone-do-ubuntu-pelo-terminal-2.html)