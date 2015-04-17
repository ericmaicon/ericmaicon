title: "Killing the audio process in a Mac OS"
date: 2015-04-17 18:01:06
categories:
- MacOS
tags:
- MacOS
---
![MacOS](/thumbnails/apple.php)

Did your audio leak and don't you know what to do in your MacOS? I had a problem where I was coding and suddenly the audio leaked and stopped. It happened several times a day, so the restart process would not be a good approach.

If you know how to use the terminal in a MacOS, you can use the following command to kill the process and start to listen again:

```sh
sudo kill -9 `ps ax|grep 'coreaudio[a-z]' | awk '{print $1}’`
```

It will request your password. After that, the audio would work again.