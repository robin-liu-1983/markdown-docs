# Ubuntu14.04搭建pptp类型vpn服务器
<!-- toc -->

- [Ubuntu14.04搭建pptp类型vpn服务器](#ubuntu1404搭建pptp类型vpn服务器)
  - [1. 购置虚拟主机](#1-购置虚拟主机)
  - [2. 安装pptp软件](#2-安装pptp软件)
  - [3. 配置pptp：](#3-配置pptp)
    - [3.1 配置pptp.conf](#31-配置pptpconf)
    - [3.2 配置pptpd-option中的DNS](#32-配置pptpd-option中的dns)
    - [3.3 设置账号密码：](#33-设置账号密码)
    - [3.4 重启pptp服务：](#34-重启pptp服务)

  - [4. 配置iptables](#4-配置iptables)
    - [4.1 设置ipv4转发:](#41-设置ipv4转发)
    - [4.2 安装iptables](#42-安装iptables)
    - [4.3 添加NAT规则](#43-添加nat规则)
    - [4.4 保存iptables规则，并在开机加载网卡时自动加载规则](#44-保存iptables规则并在开机加载网卡时自动加载规则)

  - [5. 监控VPN](#5-监控vpn)
  - [6. 方法VPN](#6-方法vpn)
<!-- tocstop -->

在国内想要上facebook、twitter等社交网站，想要用google进行搜索，想要看youtube的视频，就需要具有翻墙这项特殊的技能。翻墙的方法有许多，购买vpn，使用goagent，当相比之下使用pptp搭建自己的vpn是最为稳定和快速的。

> 虚拟专用网络（Virtual Private Network ，简称VPN)指的是在公用网络上建立专用网络的技术。它涵盖了跨共享网络或公共网络的封装、加密和身份验证链接的专用网络的扩展。VPN主要采用了彩隧道技术、加解密技术、密钥管理技术和使用者与设备身份认证技术。

> 点对点隧道协议（PPTP）是VPN服务的一种最简单的实现协议，其它常见的VPN类型还有：使用IPsec的第2层隧道协议（L2TP/IPsec）、安全套接字隧道协议（SSL VPN）。

## 1. 购置虚拟主机
目前虚拟主机很多，AWS，阿里云，linode等等。我选择的是阿里云刚推出的主机在新加坡的虚拟服务器，并购买了域名，加上优惠码，平均一个月100元左右，上行1M，性能相当好，我在上面除了个人主页，vpn外要有对国外社交网站的分析试验，速度相当不错，强烈推荐。

为什么选择阿里云，主要是国内模仿AWS最想的云平台，提供的服务相当全面，在新加坡的主机服务器，国内访问速度比AWS快很多，达到200～300K，下载速度在3M左右，访问国际网络速度也很好，而且申请的域名不用备案。

## 2. 安装pptp软件

```
$ sudo apt-get update && sudo apt-get upgrade
$ sudo apt-get install pptpd
$ alias ec="emacsclient -d"
```

## 3. 配置pptp：
### 3.1 配置pptp.conf

```
$ sudo ec /etc/pptpd.conf
...
#localip 192.168.0.1                    ＃去掉这两行注释
#remoteip 192.168.0.234-238,192.168.0.245
...
```

### 3.2 配置pptpd-option中的DNS

```
$ sudo ec /etc/ppp/pptpd-options
```

添加Google的DNS：

```
ms-dns 8.8.8.8
ms-dns 8.8.4.4
```

### 3.3 设置账号密码：

```
$ sudo ec /etc/ppp/chap-secrets
```

添加一行，依次为：

```
#用户名     服务          密码          限制IP：
user            pptpd       password    *
```

### 3.4 重启pptp服务：

```
$ sudo /etc/init.d/pptpd restart
```

## 4. 配置iptables
### 4.1 设置ipv4转发:

```
$ sudo ec /etc/sysctl.conf
```

添加

```
net.ipv4.ip_forward=1
```

```
$ sudo sysctl -p
```

### 4.2 安装iptables

```
$ sudo apt-get install iptables
```

### 4.3 添加NAT规则

```
$ sudo iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o eth1 -j MASQUERADE
```

设置MTU，防止包过大：

```
$ sudo iptables -A FORWARD -s 192.168.0.0/24 -p tcp -m tcp --tcp-flags SYN,RST SYN -j TCPMSS --set-mss 1200
```

### 4.4 保存iptables规则，并在开机加载网卡时自动加载规则

```
$ sudo iptables-save > /etc/iptables-rules
```

```
$ sudo ec /etc/network/interfaces
```

在文件末尾加入：

```
pre-up iptables-restore < /etc/iptables-rules
```

## 5. 监控VPN
查看VPN在线用户

```
$ sudo ifconfig | grep ppp
$ last | grep still | grep ppp
```

查看VPN用户实时流量信息

```
$ sudo apt-get install ifstat
$ sudo ifstat
```

## 6. 方法VPN
我在Windows7、Mac OSX、iphone、Android手机上分别使用pptp的方式进行了使用速度很快，看视频没有问题。

**本文原创，转载请注 [狮子座流星](http://robin.info-lab.top)**
