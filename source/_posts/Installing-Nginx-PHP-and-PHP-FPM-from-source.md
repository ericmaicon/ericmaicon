title: "Installing Nginx, PHP and PHP-FPM from source"
date: 2015-04-17 18:07:06
categories:
- PHP
tags:
- PHP
---
![PHP](/thumbnails/php.jpg)

You may want to choose your exactly PHP configuration and extra components when you are creating a PHP server, right? To do so, the best approach is installing from the source.

A good advice when you are installing from the source is: **install first all dependencies** (MySQL, PostgreSQL, Oracle, mcrypt ...) and just after that, you should install the PHP. Why? Because some PHP components use some headers and files from these dependencies, it will avoid an error when the PHP starts to compile.

I am using a Debian distribution. I tried to use few things from package management. It may be easy for you to replace the following part to another distribution.

Let's start updating the aptitude and installing the basic requirements:

```sh
aptitude update
aptitude install build-essential libaio-dev libltdl-dev libltdl7
```

Now, the step 2 is start to install all dependencies.

### FreeTDS - MS SQL

If you want to work with SQL Server + PHP, you need to install the [FreeTDS](http://www.freetds.org/) application.

```sh
cd /usr/src/
wget ftp://ftp.astron.com/pub/freetds/stable/freetds-stable.tgz
tar zxvf freetds-stable.tgz
cd freetds-0.91
./configure --with-tdsver=8.0 --enable-msdblib --with-gnu-ld --enable-shared --enable-static --prefix=/usr/local/freetds
make && make install
```

### Instant Client - Oracle

If you want to work with Oracle + PHP, you need to install the instant client for Oracle. There isn't a good way to download it by wget. To do so, you need to enter in the oracle site, accept the license, and download it.

1. Open the [Oracle Download Page](http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html)
2. Choose the right version of your instant client (It is very important to choose the same architecture of your OS, otherwise you will have error when the PHP starts to communicate with it):

![Instant Client](/images/Installing-Nginx-and-PHP-from-source.png)

3. Accept the license:

![Instant Client](/images/Installing-Nginx-and-PHP-from-source-2.png)

4. Download the basic version:

![Instant Client](/images/Installing-Nginx-and-PHP-from-source-3.png)

5. Download the sdk version:

![Instant Client](/images/Installing-Nginx-and-PHP-from-source-4.png)

After that, you should upload these files to your server.

```sh
unzip instantclient-basic-linux.x64-11.2.0.3.0.zip
unzip instantclient-sdk-linux.x64-11.2.0.3.0.zip
mv instantclient_12-1/ /usr/local/oracle-client-12-1

ln -s /usr/local/oracle-client-12-1/libclntsh.so.11.1 /usr/local/oracle-client-12-1/libclntsh.so
ln -s /usr/local/oracle-client-12-1/libocci.so.11.1 /usr/local/oracle-client-12-1/libocci.so

export ORACLE_HOME=/usr/local/oracle-client-12-1
export LD_LIBRARY_PATH=/usr/local/oracle-client-12-1
```

At the script above, you need to take care with the name of these files. You may need to check the version that you download and change the file name at the script. Your instant client is ready to work with PHP.

### Ioncube

[Ioncube](http://www.ioncube.com) is a software that encrypt/decrypt your code. It allows you to send a code to a customer without send the source.

Your server just need the loader to allow it decrypt those encrypted files:

```sh
cd /usr/src
wget http://downloads2.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz
tar zxvf ioncube_loaders_lin_x86-64.tar.gz
cp -R ioncube /usr/local 
```

### PHP Dependencies

All dependencies listed below aren't required. Besides that, a great PHP Server always requires GD, cURL, and SSL. To do so, I put those dependecies.


#### Lib XML

```sh
cd /usr/src
wget http://xmlsoft.org/sources/libxml2-2.7.2.tar.gz
tar zxvf libxml2-2.7.2.tar.gz
cd libxml2-2.7.2
./configure
make && make install
```

#### cURL

```sh
cd /usr/src
wget http://curl.haxx.se/download/curl-7.27.0.tar.gz
tar zxvf curl-7.27.0.tar.gz
cd curl-7.27.0
./configure
make && make install
```

#### OpenSSL

```sh
cd /usr/src
wget http://www.openssl.org/source/openssl-1.0.1g.tar.gz
tar zxvf openssl-1.0.1g.tar.gz
cd openssl-1.0.1g
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
make && make install
```

If you want to check the installation, you can run the follow command:

```sh
/usr/local/openssl/bin/openssl version
OpenSSL 1.0.1g 7 Apr 2014
```

#### Free Type

```sh
cd /usr/src
wget http://download.videolan.org/contrib/freetype-2.5.3.tar.gz
tar zxvf freetype-2.5.3.tar.gz
cd freetype-2.5.3
./configure
make && make install
```

#### JPEG

```sh
cd /usr/src
wget http://fossies.org/linux/misc/jpegsrc.v9a.tar.gz
tar zxvf jpegsrc.v9a.tar.gz
cd jpeg-9a
./configure
make && make install
```

#### lib PNG

```sh
cd /usr/src
wget http://78.108.103.11/MIRROR/ftp/png/src/history/libpng16/libpng-1.6.16.tar.gz
tar zxvf libpng-1.6.16.tar.gz
cd libpng-1.6.16
./configure
make && make install
```

#### zlib

```sh
cd /usr/src
wget http://zlib.net/zlib-1.2.8.tar.gz
tar zxvf zlib-1.2.8.tar.gz
cd zlib-1.2.8
./configure
make && make install
```

#mcrypt

```sh
cd /usr/src
wget https://vps.googlecode.com/files/libmcrypt-2.5.8.tar.gz
tar -zxvf libmcrypt-2.5.8.tar.gz
cd libmcrypt-2.5.8
./configure --prefix=/usr/local  --disable-posix-threads --enable-dynamic-loading
make && make install
```

### PHP

Let's install our PHP.

```sh
cd /usr/src
wget http://br2.php.net/distributions/php-5.5.12.tar.gz
tar zxvf php-5.5.12.tar.gz
cd php-5.5.12
```

If you did everything right until here, you may don't have any trouble. Some errors may appear at the command below. The cause of those errors would be because of some missing dependency or library. Review the installation of those dependencies above, if they have the same architecture of your OS.

```sh 
./configure  --prefix=/usr/local/php \
             --with-config-file-path=/usr/local/php/etc \
             --with-zlib \
             --with-curl=/usr/src/curl \
             --enable-mbstring \
             --with-openssl=/usr \
             --enable-fpm \
             --enable-soap \
             --enable-calendar \
             --enable-sockets \
             --enable-zip \
             --disable-debug \
             --with-jpeg-dir=/usr/local/lib \
             --with-freetype-dir \
             --enable-gd-native-ttf \
             --with-png-dir=/usr/local/libpng-1.6.10 \
             --with-gd \
             --with-libdir=/lib/x86_64-linux-gnu \
             --with-mcrypt
```

**Important notes:**

1. I used a 64bits architecture OS. The command below will allow PHP source to use those 64 libs files.

```sh
--with-libdir=/lib/x86_64-linux-gnu \
```

2. To install with FreeTDS support, you must add the following param:

```sh
--with-pdo-dblib=/usr/local/freetds/ \
```

3. To install with Oracle support, you must add these following params:

```sh
--with-oci8=instantclient,/usr/local/oracle-client-12-1 \
--with-pdo-oci=instantclient,/usr/local/oracle-client-11-2,10.2.0.4.0 \
```

4. To install with PostgreSQL support, you must add the following param.

```
--with-pdo-pgsql \
```

You would need an extra library installed in your server. If you installed the PostgreSQL by source, you would already have it, otherwise you will receive the following error:

```
libpq-fe.h: No such file or directory
```

You can fix this installing the postgresql-dev package.


5. To install with MySQL support, you must add these following params.

```sh
--with-mysql \
--with-pdo-mysql
```

You would need an extra library installed in your server. If you installed the MySQL by source, you would alread have it, otherwise you will receive the following error:

```
error: Cannot find MySQL header files under /usr/include/mysql.
```

You can fix this installing the mysql-dev package.

**CentOS**:
```sh
yum install mysql-devel
```

**Debian**:
```sh
aptitude install libmysqld-dev
```


After that, if your configure command runned with success, you are able to run the make command:

```sh
make && make install
```

Congratulations. We installed the PHP from the source with all those dependencies that you want.

### Nginx Depencencies

#### PCRE

```sh
cd /usr/src
wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.31.tar.gz
tar zxvf pcre-8.31.tar.gz
cd pcre-8.31
./configure
make && make install
```

### Nginx

[Nginx](http://nginx.org/) is an HTTP server. If well configured, it would be more faster than Apache. To install it:

```sh
cd /usr/src
wget http://nginx.org/download/nginx-1.1.6.tar.gz
tar -zxvf nginx-1.1.6.tar.gz
cd nginx-1.1.6
./configure --without-mail_pop3_module --without-mail_imap_module --without-mail_smtp_module --with-http_stub_status_module
make && make install
```

### Configuring PHP to works with Nginx.

To configure Nginx to work with, you just need to change the nginx.conf:

```
vi /usr/local/nginx/conf/nginx.conf
```

```
server {
    listen      80;
    server_name localhost;
    root        /var/www;
    autoindex   on;
    index       index.php index.html index.htm;

    location ~ \.php {
        fastcgi_pass 127.0.0.1:9000;
    }
}
```

After that, you just need some scripts to start/stop PHP-FPM and Nginx. You may find a link to download each script below:

* [nginx](https://gist.github.com/ericmaicon/cb6ab18a6409a27cfadb)
* [php-fpm](https://gist.github.com/ericmaicon/4c97bd9a23eac6b3d0fa)
* [php-fpm.conf](https://gist.github.com/ericmaicon/0f44e3b2213522a90e40)

Download nginx and php-fpm script and put inside of /etc/init.d directory. Download php-fpm.conf and put it inside of /usr/local/php/etc/ directory.

```sh
chmod +x /etc/init.d/php-fpm
chmod +x /etc/init.d/nginx

/etc/init.d/php-fpm start
/etc/init.d/nginx start
```

**Note:**

If you are running the instantclient with oracle, you need to change the /usr/local/nginx/conf/fastcgi_params file and increase:

```
fastcgi_param                LD_LIBRARY_PATH   "/usr/local/oracle-client-12-1";
fastcgi_param                ORACLE_HOME       "/usr/local/oracle-client-12-1";
```

Your server is ready to rock.