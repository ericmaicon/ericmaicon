title: "Tip: Nginx with SSL"
date: 2015-06-20 20:16:23
categories:
- Nginx
tags:
- Nginx
---
![Nginx](/thumbnails/nginx.jpg)

A fast tip, I needed to install a SSL certificate on a Nginx server. I followed this tutorial and everything worked fine:

[https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-nginx-for-ubuntu-12-04](https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-nginx-for-ubuntu-12-04)

Those changes that I did was the configure installation of Nginx, that I used the following command:

```sh
sudo ./configure --with-http_ssl_module --with-http_gzip_static_module --with-file-aio --without-mail_pop3_module --without-mail_imap_module --without-mail_smtp_module --with-ld-opt="-L /usr/local/lib"
```

And the another one was the nginx config file:

```
ssl                  on;
ssl_certificate      /usr/local/nginx/conf/cert/site.crt;
ssl_certificate_key  /usr/local/nginx/conf/cert/site.key;
ssl_session_timeout  5m;
ssl_protocols  SSLv2 SSLv3 TLSv1;
ssl_ciphers  HIGH:!aNULL:!MD5;
ssl_prefer_server_ciphers   on;

location / {
    try_files $uri $uri/ /index.php?$args;
}

location ~ \.php$ {
    fastcgi_pass 127.0.0.1:9000;
}
```

Enjoy!