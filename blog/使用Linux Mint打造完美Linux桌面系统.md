# 使用Linux Mint打造完美Linux桌面环境
作为一个使用Linux近三年的用户，对于桌面版本和服务器版本都算比较熟悉。

尝试使用了服务器版本有CentOS5，CentOS6，Debian5，Debian6和Ubuntu10.04，使用的桌面版本有Fedora17，Ubuntu12.10，Mageia2，OpenSuse12.2，LinuxMint14，桌面环境有Gnome3，Gnome2，Xface和KDE。

通过比较服务器版本使用CentOS6和Debian6十分的高效和稳定，桌面版本使用LinuxMint14和Mageia2十分符合用户习惯。但Mageia2还不是很稳定而且驱动也不是十分齐全。如我添加打印机后，dbus报错，无法使用中文输入法;AMD Randon2400显卡驱动不稳定无法实现双屏显示。

LinuxMint14就没有这些问题，十分适合Windows用户转型到Linux上，驱动完善，软件丰富，唯一的缺点就是对于国内用户来说，需要进行一下优化处理，本文就是对于整个处理过程进行介绍。

Linux Mint是基于Ubuntu（基于Debian）开发的Linux系统，在Distrowatch排行榜第一名Linux发行版本。该系统继承了Ubuntu的众多有点，同时在Ubuntu的基础上加入了很多优秀的特性。目标是提供一种开箱即用的用户体验，免去用户需要自行安装一系列满足基本使用需求的软件，包括浏览器flash插件、多媒体编码器、对DVD的支持、Java及其他组件。

Linux Mint 14 新特点：Mate1.4 (Mate是基于Gnome2融合Gnome2和gnome3的桌面环境)，cinnamon1.6 (cinnamon是linux mint创始的桌面交互环境，它基于gnome shell提供类似于gnome2的布局和丰富的桌面特效自定义)，自定义mdm，加强的software manager。

1、使用更加快速的更新源。 使用中国科技大学的镜像服务器：mirrors.ustc.edu.cn. 编辑/etc/apt/sources.list

```
deb http://mirrors.ustc.edu.cn/linuxmint/ nadia main upstream import backport
deb http://mirrors.ustc.edu.cn/ubuntu/ quantal main restricted universe multiverse
deb http://mirrors.ustc.edu.cn/ubuntu/ quantal-updates main restricted universe multiverse
deb http://mirrors.ustc.edu.cn/ubuntu/ quantal-security main restricted universe multiverse
```

其中第一行为linuxmint更新，后三个为ubuntu更新。编辑完成后，使用

```
sudo apt-get update; apt-get upgrade
```

2、添加中文输入法fcitx，使用 sudo apt-get install fcitx fcitx-pinyin. 在控制中心中修改输入法切换器为fcitx，修改fcitx配置。注销后重新登录就可以使用中文输入法了。

3、其他设置。使用双显示器，修改显示器配置。修改外观，电源管理，屏幕保护，桌面设置，登录窗口，添加打印机。

4、安装软件。Linux Mint有三种方式安装软件：使用新得立软件管理器，Mint软件管理器和apt-get。其中Mint软件管理器最为直观，而apt-get最为高效。我们使用apt-get来安装软件。

Graphics: GIMP        Shotwell    Picasa

Internet: Firefox        Opera        chromium    Flash player Filezilla    Thunderbird    Evolution    aMule Transmission    Vuze        Pidgin        Google Earth Skype        Xchat IRC

Office: Libreoffice    Adobe Reader foxit GnuCash        Scribus

Multimedia: Amarok        Audacity    Banshee        Mplayer Rhythmbox    gtkPod        XMMS        dvd::rip Movies        VLC        Totem        Xine Brasero        K3B        mutilmedia codes

Programming: Kompozer    Blue Fish    Eclispe        Emacs

Other: VirtualBox-ose    True Type fonts    Java        Read/Write suport for NTFS partitions

```
#multi-media
sudo apt-get install amule vuze skype googleearth gnucash scribus amarok audacity sound-juicer normalize-audio sox vcdimager virtualbox-ose eclipse
```

```
#office
sudo apt-get install debuge rhythmbox libreoffice gwibber evince conky-all devede firestarter
```

```
#programming
sudo apt-get install unetbootin keepassx mc clamav gtkhash htop leafpad geany monodevelop codeblocks qtcreator git-core subversion build-essential mercurial codelite geany-plugins  glade scala sqlitebrowser cmake maven2 monkeystudio vinagre  rsync inkscape filezilla shotwell chromium-browser bluefish gtkpod dvdrip vlc xine-ui xine-plugin k3b lyx scite diffuse bless emesene evolution wireshark openssh-server putty gftp zenmap webhttrack remmina
```

```
#game
sudo apt-get install worldofgoodemo wesnoth frozen-bubble warzone2100 supertuxkart hedgewars
```

5、安装chrome。作为最为快速和易用的浏览器，不能没有chrome。下载地址: [https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb](https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb) [https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.rpm](https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.rpm)

6、美化linux。安装oxygen-gtk主题，apt-get install gtk2-engine-oxygen-gtk。外观首选项，自定义主题，选择oxygen-gtk。
