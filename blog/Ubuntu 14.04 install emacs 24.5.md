# Ubuntu-14.04-install-emacs-24.5
<!-- toc -->

- [Ubuntu-14.04-install-emacs-24.5](#ubuntu-1404-install-emacs-245)
  - [1. 前期准备工作](#1-前期准备工作)
  - [2. 安装基础构件工具](#2-安装基础构件工具)
  - [3.下载emacs编译需要的依赖库](#3下载emacs编译需要的依赖库)
  - [4.下载emacs24.5编译安装](#4下载emacs245编译安装)
  - [5.下载并安装我的emacs配置文件](#5下载并安装我的emacs配置文件)
  - [6. 配置tmux和zsh](#6-配置tmux和zsh)
<!-- tocstop -->

## 1. 前期准备工作
在阿里云创建虚拟主机 操作系统Ubuntu 14.04 STL 修改更新源，更新系统，安装必要软件

```bash
$ cd /etc/apt
$ wget -c http://mirrors.163.com/.help/sources.list.trusty
$ mv sources.list sources.list.bak
$ mv sources.list.trusty sources.list
$ apt-get update
$ apt-get upgrade
$ apt-get install git zsh tmux curl
```

## 2. 安装基础构件工具

```bash
$ sudo apt-get install build-essential
```

## 3.下载emacs编译需要的依赖库

```bash
sudo apt-get build-dep emacs24
```

## 4.下载emacs24.5编译安装

```bash
wget -c http://ftp.gnu.org/gnu/emacs/emacs-24.5.tar.gz
tar zxf emacs-24.5.tar.gz
./configure  --with-x-toolkit=no
make
make install
```

## 5.下载并安装我的emacs配置文件

```bash
git clone https://github.com/robin-liu-1983/emacs-robin.d.git
cd emacs-robin.d
cp -rf emacs.d ~/.emacs.d
```

## 6. 配置tmux和zsh

```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
cp tmux.conf ~/.tmux.conf
cp zshrc-linux ~/.zshrc
```

**本文原创，转载请注 [狮子座流星](http://robin.info-lab.top)**
