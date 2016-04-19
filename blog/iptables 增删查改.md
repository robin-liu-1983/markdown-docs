# iptables增删查改
<!-- toc -->

- [iptables增删查改](#iptables增删查改)
  - [一.安装并启动防火墙](#一安装并启动防火墙)
    - [1.添加filter表](#1添加filter表)
    - [2.添加NAT表](#2添加nat表)
    - [3. 指定位置添加](#3-指定位置添加)

  - [三.删除iptables规则](#三删除iptables规则)
  - [四.查看防火墙规则](#四查看防火墙规则)
    - [1.查看filter表](#1查看filter表)
    - [2.查看nat表](#2查看nat表)

  - [五.修改规则](#五修改规则)
  - [六. 设置默认规则](#六-设置默认规则)
<!-- tocstop -->

iptables是linux系统自带的防火墙，功能强大。如果iptables不熟悉的话可以用apf，是一款基于iptables的防火墙。

## 一.安装并启动防火墙

```
$ /etc/init.d/iptables start
```

当我们用iptables添加规则，保存后，这些规则以文件的形势存在磁盘上的，以centos为例，文件地址是/etc/sysconfig/iptables，我们可以通过命令的方式去添加，修改，删除规则，也可以直接修改/etc/sysconfig/iptables这个文件就行了。

## 二.添加防火墙规则
### 1.添加filter表

```
$ iptables -A INPUT -p tcp -m tcp --dport 21 -j ACCEPT
```

-dport 开放21端口 -A 默认是插入到尾部的(add)

### 2.添加NAT表

```
$ iptables -t nat -A POSTROUTING -s 192.168.10.0/24 -j MASQUERADE
```

将源地址是 192.168.10.0/24 的数据包进行地址伪装 -t 类型 (type)

### 3. 指定位置添加

```
$ iptables -I INPUT 3 -p tcp -m tcp --dport 20 -j ACCEPT
$ iptables -L -n --line-number
Chain INPUT (policy DROP)
num  target     prot opt source               destination
1    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0
2    DROP       icmp --  0.0.0.0/0            0.0.0.0/0           icmp type 8
3    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           tcp dpt:20
```

-L 列出 list --line-number 显示行号 -I指定位置添加

## 三.删除iptables规则

```
$ iptables -D INPUT 3               #删除input的第3条规则
```

```
$ iptables -t nat -D POSTROUTING 1      #删除nat表中postrouting的第一条规则
$ iptables -F INPUT             #清空 filter表INPUT所有规则
$ iptables -F                           #清空所有规则
$ iptables -t nat -F POSTROUTING        #清空nat表POSTROUTING所有规则
```

## 四.查看防火墙规则
### 1.查看filter表

```
$ iptables -L -n --line-number |grep 21
```

如果不加-t的话，默认就是filter表，查看，添加，删除都是的

### 2.查看nat表

```
$ iptables -t nat -vnL POSTROUTING --line-number
```

## 五.修改规则

```
$ iptables -R INPUT 3 -j DROP                       #-R  将规则3删除
```

## 六. 设置默认规则

```
$ iptables -P INPUT DROP                        #设置filter表INPUT默认规则是 DROP
```

所有添加，删除，修改后都要保存起来，

```
$/etc/init.d/iptables-save
```

**本文原创，转载请注 [狮子座流星](http://robin.info-lab.top)**
