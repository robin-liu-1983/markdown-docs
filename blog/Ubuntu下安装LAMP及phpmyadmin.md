# Ubuntu下安装LAMP及phpmyadmin
<!-- toc -->

- [Ubuntu下安装LAMP及phpmyadmin](#ubuntu下安装lamp及phpmyadmin)
	- [1.安装 Apache](#1安装-apache)
	- [2.安装 PHP5](#2安装-php5)
	- [3.安装 MySQL](#3安装-mysql)
	- [4、安装phpmyadmin](#4-安装phpmyadmin)

<!-- tocstop -->

关于Ubuntu下的LAMP配置，已经成为了某一些人的心病，加上phpmyadmin的配置，更是使他们不知所以。现在我就把我在LINUX 下的关于配置LAMP 及phpmyadmin 的一些经验，分享一下。希望对你有些帮助。

我们首先要安装LAMP 就是Apache,PHP5,Mysql5，Perl5.

打开终端，输入命令行。

## 1.安装 Apache

```
sudo apt-get install apache2
```

[http://localhost/](http://localhost/)

## 2.安装 PHP5

```
sudo apt-get install php5 libapache2-mod-php5
```

```
sudo service apache2 restart
```

```
sudo emacs /var/www/phpinfo.php
```

`<?php phpinfo(); ?>`

[http://localhost/phpinfo.php](http://localhost/phpinfo.php)

显示出PHP的信息内容页面，说明你又成功了一小步。

## 3.安装 MySQL

```
sudo apt-get install mysql-server mysql-client
```

```
mysql -u root
```

```
mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('yourpassword');
```

以上的'root'是用户名，'yourpassword'是密码。

## 4、安装phpmyadmin

```
sudo apt-get install php5-mysql phpmyadmin
```

```
cp /etc/phpmyadmin/apache.conf /etc/apache2/sites-available/phpmyadmin.conf
```

[http://localhost/phpmyadmin](http://localhost/phpmyadmin)

```
sudo a2ensite phpmyadmin
```

```
sudo /etc/init.d/apache2 restart
```

[http://localhost/phpmyadmin](http://localhost/phpmyadmin)
