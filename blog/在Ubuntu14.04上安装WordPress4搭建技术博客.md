# 在Ubuntu14.04上安装WordPress4搭建技术博客


<!-- toc -->

- [在Ubuntu14.04上安装WordPress4搭建技术博客](#在ubuntu1404上安装wordpress4搭建技术博客)
	- [1. 安装LAMP环境](#1-安装lamp环境)
		- [1.1 安装Apache2](#11-安装apache2)
		- [1.2 安装MySQL5](#12-安装mysql5)
		- [1.3 安装PHP5](#13-安装php5)
		- [1.4 安装phpMyAdmin](#14-安装phpmyadmin)
	- [2. 初始化数据库](#2-初始化数据库)
	- [3. 下载并配置WordPress](#3-下载并配置wordpress)
	- [4. 配置Apache服务器](#4-配置apache服务器)
	- [5. 安装WordPress](#5-安装wordpress)
	- [6. 设置主题（themes）](#6-设置主题themes)
	- [7. 设置固定链接（Permalinks）](#7-设置固定链接permalinks)
	- [8. 安装插件](#8-安装插件)
		- [8.1 JetPack插件](#81-jetpack插件)
		- [8.2 Google Analytics Dashboard插件](#82-google-analytics-dashboard插件)
		- [8.3 Menu Social Icons插件](#83-menu-social-icons插件)
		- [8.4 安装WP Super Cache插件](#84-安装wp-super-cache插件)
	- [9. 使用Markdown发布文章](#9-使用markdown发布文章)
	- [10. WP备份和恢复](#10-wp备份和恢复)

<!-- tocstop -->


搭建自己的技术博客有许多方式，可以在cnblogs上搭建，可以在新浪博客上搭建，还可以在wordpress.com上搭建。但终归不如在自己的ubuntu虚拟主机上使用WordPress(简称WP)搭建一个，使用起来顺手，可以完全定制。

>博客（英语：Blog，为Web Log的混成词），意指log on the web意即在网络上纪录，是一种由个人管理、张贴新的文章、图片或视频的网站或在线日记，用来纪录、抒发情感或分享信息[1]。博客上的文章通常根据张贴时间（Chronological Order），以倒序方式由新到旧排列。

>许多博客作者专注评论特定的课题或新闻，其他则作为个人日记。一个典型的博客结合了文字、图像、其他博客或网站的超链接、及其它与主题相关的媒体。能够让读者以互动的方式留下意见，是许多博客的重要要素。大部分的博客内容以文字为主，仍有一些博客专注在艺术、摄影、视频、音乐、播客等各种主题。博客是社会媒体网络的一部分。

## 1. 安装LAMP环境

LAMP 是Linux, Apache, MySQL, PHP, perl的缩写. 指在linux上安装Apache2，MySQL, PHP等软件包所建立的网站运行平台，是目前中小网站主要的运行环境。

### 1.1 安装Apache2

```
$ sudo apt-get install apache2
```

### 1.2 安装MySQL5

```
$ sudo apt-get install mysql-server mysql-client
```

中途需要设置root密码

### 1.3 安装PHP5

```
$ sudo apt-get install php5 libapache2-mod-php5 php5-mysql php5-curl php5-gd php5-intl php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-snmp php5-sqlite php5-tidy php5-xmlrpc php5-xsl php5-xcache libssh2-php
```

### 1.4 安装phpMyAdmin

```
$ sudo apt-get install phpmyadmin
...
Web server to reconfigure automatically: < -- apache2
Configure database for phpmyadmin with dbconfig-common? <-- No
...
```

## 2. 初始化数据库

```
$ sudo mysql -u root -p
Enter Password:
...
```

```sql
mysql>  CREATE DATABASE wordpressdb;
mysql>  CREATE USER wordpressuser@localhost IDENTIFIED BY 'wordpresspassword';
mysql>  GRANT ALL PRIVILEGES ON wordpressdb.* TO wordpressuser@localhost;
mysql> FLUSH PRIVILEGES;
mysql> exit
```

wordpress --> wp
wordpressbwst

重启服务

```
$ sudo service apache2 restart
$ sudo service mysql restart
```

## 3. 下载并配置WordPress

```
$ mkdir temp
$ cd temp
$ wget http://wordpress.org/wordpress-4.x.tar.gz
https://cn.wordpress.org/wordpress-4.4.2-zh_CN.tar.gz
$ tar zxf wordpress-4.x.tar.gz -C /var/www/html/
$ mkdir -p /var/www/html/wordpress/wp-content/uploads
```

关键更改目录权限为www-data www-data

```
$ sudo chown -R www-data.www-data /var/www/html/wordpress
$ sudo chmod -R 755 /var/www/html/wordpress
$ sudo chown -R :www-data /var/www/html/wordpress/wp-content/uploads
```

配置wp-config.php

```
$ cd /var/www/html/wordpress/
$ cp wp-config-sample.php wp-config.php
$ emacs wp-config.php

#wp-config.php
...
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpressdb');
/** MySQL database username */
define('DB_USER', 'wordpressuser');
/** MySQL database password */
define('DB_PASSWORD', 'wordpresspassword');
...
```


## 4. 配置Apache服务器

在我的虚拟主机上一个IP配置了两个域名, 其中一个是blog.example.com, 我将其作为我的博客的域名。

在/etc/apache2/sites-available/目录下复制一份001-default.conf命名为wordpress.conf，进行修改第一行*:80 为blog.example.com:80，启用这个网站，重启apache服务。

```
$ sudo emacs /etc/apache2/sites-available/wordpress.conf

#wordpress.conf
<virtualhost blog.example.com:80>
...
ServerName blog.example.com

$ sudo a2ensite wordpress
$ sudo service apache2 restart
```

域名解析

创建.htaccess文件

```
$ sudo touch /var/www/html/wordpress/.htaccess
$ sudo chown www-data:www-data /var/www/html/wordpress/.htaccess
$ sudo chmod 664 /var/www/html/wordpress/.htaccess
```

## 5. 安装WordPress

用浏览器打开 http://blog.example.com/ , 一步一步安装WP

## 6. 设置主题（themes）

我选用默认的**Twenty Fifteen**主题，在定制中进行了配置：

* 修改**站点身份**中**站点图标**为我的头像
*  修改**顶部图像**
*  添加了一些**小工具**

## 7. 设置固定链接（Permalinks）

在**设置**中的**固定链接**中设置
我选用的是**文章名**
分类目录前缀我的是**topics**

## 8. 安装插件

WP安装难免需要安装插件以提供更多的功能。下面为大家推荐几款：

### 8.1 JetPack插件

JetPack插件是**wordpress.com**公司自行推出的一款插件，功能十分强大，可以用来单点登录，站点统计，添加twitter等社交网站的共享图标，可以自动在各大社交网站上进行博客推广，可以支持Markdown发布文章，可以添加很多小组件，还可以在文章中轻松插入公式，实在是居家必备。

### 8.2 Google Analytics Dashboard插件

Google Analytics Dashboard插件，是通过Google Analytics对网站进行统计分析，分析的项目十分详尽，需要进行一下身份认证。

### 8.3 Menu Social Icons插件

在wordpress4 以后出现了**社交网络链接菜单**，这个功能可相当好用，可以使用社交网络图标配合自己的社交网络id形成链接菜单。但配置有些繁琐，使用Menu Social Icons插件，就可以不费吹灰之力，建立自己的社交网络链接菜单了。

### 8.4 安装WP Super Cache插件

生成静态缓存页面是提高网站访问性能的重要方式，使用**WP Super Cache插件**可以快速的生成网页的静态缓存，性能优异。

## 9. 使用Markdown发布文章

安装了JatPack插件后就可以用Markdown发布文章了。
我目前发布文章的方式是，

1. 在本地用**MacDown**先写好文章，该软件同时可以同步预览，十分好用。
2. 使用wordpress推出的**wordpress.com**网站管理工具进行发布。

安装了JatPack插件后，还可以输入好看的数学公式：

$$ i\hbar\frac{\partial}{\partial t}\left|\Psi(t)\right>=H\left|\Psi(t)\right> $$


## 10. WP备份和恢复

WP备份分为两个部分：

* 冷备份：通过备份SQL数据库和WP文件来备份

```
$ emacs /etc/mysql/my.cnf
#my.cnf
[mysqld]
...
log_bin
$ sudo mysqldump -u root -p --lock-all-tables --flush-logs --master-data=2 --all-databases > backup.sql         #完全备份数据库
$ sudo mysql -uroot -p
```

```SQL
mysql>set sql_log_bin=0;    #临时关闭二进制日志文件记录功能,恢复数据库
mysql>source backup.sql
mysql>set sql_log_bin=1
```

* 热备份：使用WP内部组件进行备份，导入导出工具等
**本文原创，转载请注 [狮子座流星](http://robin.info-lab.top)**
