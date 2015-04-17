title: "Listing 10 biggest files in a specific folder on linux"
date: 2015-04-17 17:47:18
categories:
- Linux
tags:
- Linux
---
![Linux](/thumbnails/linux.jpg)

I had a problem where I needed to find the biggest file in a folder. So, I found a command that allows it and works like a charm:


```sh
du -a / | sort -n -r | head -n 10
```

You can change the folder that you want to search. You need to change the "/" character to the directory that you want to:

```sh
du -a /home/eric | sort -n -r | head -n 10
```