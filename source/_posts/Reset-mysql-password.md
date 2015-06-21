title: "reset-mysql-password"
date: 2015-06-20 20:03:43
categories:
- MySQL
tags:
- MySQL
---
![MySQL](/thumbnails/mysql.jpg)

Sometimes on Linux, you need to change the MySQL password. You can do it easly following those steps below.

First of all, you need to stop the MySQL daemon.

```sh
/etc/init.d/mysql stop
```

After that, start MySQL daemon skipping the MySQL credentials process:

```sh
mysqld_safe --skip-grant-tables
```

Log in on MySQL:

```sh
mysql --user=root mysql
```

run these SQL below, where 'new-password' is the password that you want:

```sql
update user set Password=PASSWORD('new-password') where user='root';
flush privileges;
exit;
```

Done.

Source:
[https://www.howtoforge.com/reset-forgotten-mysql-root-password](https://www.howtoforge.com/reset-forgotten-mysql-root-password)