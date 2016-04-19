# Ubuntu 10.04 STL grub2 详解
<!-- toc -->

- [Ubuntu 10.04 STL grub2 详解](#ubuntu-1004-stl-grub2-详解)
  - [Grub2特性](#grub2特性)
  - [Grub2结构](#grub2结构)
  - [/etc/default/grub文件详细修改方法](#etcdefaultgrub文件详细修改方法)
    - [1、首先看下/etc/default/grub，先从应用程序－附件里打开终端，输入](#1-首先看下etcdefaultgrub先从应用程序-附件里打开终端输入)
    - [2. /etc/grub.d文件夹详细修改方法](#2-etcgrubd文件夹详细修改方法)
    - [下面第二个菜单项可删除](#下面第二个菜单项可删除)
    - [要修改默认启动项，可以使用下面的方法：](#要修改默认启动项可以使用下面的方法)
      - [第一步：打开终端，修改/etc/default/grub文件](#第一步打开终端修改etcdefaultgrub文件)
      - [第二步：修改/etc/grub.d/00_header文件](#第二步修改etcgrubd00_header文件)
      - [第三步：更新grub](#第三步更新grub)

  - [给grub2菜单添加图片](#给grub2菜单添加图片)
    - [1.在etc/grub.d文件夹中找到00_header文件，打开后在](#1在etcgrubd文件夹中找到00_header文件打开后在)
    - [2.在etc/grub.d/05_debian_theme中改为](#2在etcgrubd05_debian_theme中改为)
    - [3.根据图片位置可判断系统grub默认图片文件夹位置，在相同位置放上一张同名图片文件即可。](#3根据图片位置可判断系统grub默认图片文件夹位置在相同位置放上一张同名图片文件即可)
      - [一.修改/boot/grub/grub.cfg文件的方法（可以当作修改/etc/grub.d/文件夹和/etc/default/grub文件的参考）](#一修改bootgrubgrubcfg文件的方法可以当作修改etcgrubd文件夹和etcdefaultgrub文件的参考)

  - [二、grub2终端部分命令介绍](#二-grub2终端部分命令介绍)
    - [1.help](#1help)
    - [3.search](#3search)
    - [4.loopback](#4loopback)
    - [5.set](#5set)
    - [6.pager](#6pager)
    - [7.linux](#7linux)

  - [三、单linux系统或](#三-单linux系统或)
    - [1.开机自检后时按几下shift键，可调出菜单项](#1开机自检后时按几下shift键可调出菜单项)
    - [2.sudoupdate-grub](#2sudoupdate-grub)
    - [3.如第二种方法不能解决，直接修改grub.cfg](#3如第二种方法不能解决直接修改grubcfg)

  - [四、双硬盘双系统GrubLoading时间过长的解决方案](#四-双硬盘双系统grubloading时间过长的解决方案)
  - [五、grub2几种修复方法](#五-grub2几种修复方法)
    - [1.双系统重装windows造成grub2被改写的修复](#1双系统重装windows造成grub2被改写的修复)
      - [方法一 grub4dos0.4.4](#方法一-grub4dos044)
      - [方法二 进入Livecd后修复（感谢billbear）](#方法二-进入livecd后修复感谢billbear)

    - [2.由于root分区uuid改变造成的不能正常启动，只能进入grubrescue模式的修复](#2由于root分区uuid改变造成的不能正常启动只能进入grubrescue模式的修复)
    - [3.grub模块和配置文件grub.cfg受损无法启动时修复](#3grub模块和配置文件grubcfg受损无法启动时修复)

  - [六、另一些补充说明](#六-另一些补充说明)
    - [1.chainloader](#1chainloader)
    - [2.drivemap](#2drivemap)
    - [3.grub2引导软盘img镜像启动](#3grub2引导软盘img镜像启动)
<!-- tocstop -->

在早期的Ubuntu中，使用Grub作为系统的启动引导程序，想修改系统启动项非常简单，只要用gedit打开系统菜单设定文件（sudogedit/boot/grub/menu.lst），修改该文件中到内容即可，但是到了Grub2中，不能采用这种方式修改系统启动项了。

## Grub2特性
Grub2（GRandUnifiedBootloader,version2）是Grub的第二版。Grub2对Grub的接口进行了完整到重写，基于PUPA（详细介绍）项目到研究，Grub2更模块化并且更方便扩展，Grub2的一些提升如下：
- 具有图形化界面，支持主题
- 模块化加载
- 夸平台的兼容性
- 自定义的启动项目定义
- 修改分区命名

## Grub2结构
Grub2包含下面几个部分：
- /boot/grub/grub.cfg文件
- /etc/grub.d/文件夹
- /etc/default/grub文件

下面开始一个个介绍。

grub.cfg类似Grub中的/boot/grub/menu.lst。里面的格式于menu.lst差不多，但是现在不允许你通过直接修改该文件到方式来修改启动项，因为该文件是在执行"update-grub"或者update-grub2"之后，根据上面说到2、3两项动态生成到，也就是说，如果你修改了这个文件当下次这两个命令被执行了（比如说更新内核后），你修改到内容就会背覆盖。

/boot/grub/grub.cfg不要手工修改，这个文件是运行update-grub自动生成的。要修改配置文件的只要打开/boot/grub/grub.cfg文件，找到想修改的地方，然后根据注释找到相应的/etc/default/grub或/etc/grub.d/(folder)进行修改。

grub.cfg文件中主要包含两个部分，一部分是各个启动项的定义，第二部分是启动界面的设置。你可以直接用gedit打开该文件看其中的内容。既然grub.cfg不能修改，那也没什么好详细说的了，稍微研究下就能看懂里面是怎么写的。下面就介绍一下Grub2的另外两个部分。 Grub2的另外两部分内容其实就分别对应于grub.cfg中的两部分内容。

首先/etc/grub.d/文件夹中定义各个启动项，其中的文件代表了一个或多个启动项，命名规范都是"两个数字_名称"，前面的两位数字确定这个或这多个启动项在启动界面的位置，默认的"00_"是预留给"00_header"的，"10_是预留给当前系统内核的，20_是预留给第三方程序的，除了这些你都可以使用，增加自己的，比如05_,15_，数字越小越前面。这里的文件好像是代码，我还没研究透，不会自己写，只会改。

当执行前面说的"update-grub"或者update-grub2"命令之后，这个文件夹中的文件就是用于生成grub.cfg中启动项的定义的。 Grub2的最后一部分是/etc/default/grub文件，该文件主要是启动界面的配置，比如默认的启动项，等待用户选择启动项的时间等。文件内容很简单，就是一些键值对，详细的可配置属性可以参考Grub2的Wiki中"grub(/etc/default/grub)"这一节。当执行前面说的"update-grub"或者update-grub2"命令之后，这个文件的内容就用于生成grub.cfg中启动界面的设置。

## /etc/default/grub文件详细修改方法

```bash
sudo vim /etc/default/grub
```

系统安装完成后，用户就会发现/boot/grub/grub.cfg文件只有root权限可读，如果要直接修改grub.cfg文件，要先修改其权限。好不容易把grub.cfg修改好了，系统内核或grub升级时，会自动执行update-grub，grub.cfg文件就会被打回原形，如何保证修改后的配置文件能一直保留下来呢？

其实不用修改grub.cfg，只要把个性化配置写入/etc/default/目录下的grub和/etc/gurb.d目录下的脚本文件，以后不管升级内核或者是升级grub所执行的update-grub，都会按要求创建个性化的grub.cfg。

### 1、首先看下/etc/default/grub，先从应用程序－附件里打开终端，输入
看看打开的文件可作什么修改：

```bash
#Ifyouchangethisfile,run'update-grub'afterwardstoupdate
#/boot/grub/grub.cfg.

GRUB_DEFAULT=0-------->设置默认启动项，按menuentry顺序。比如要默认从第四个菜单项启动，数字改为3，若改为saved，则默认为上次启动项。

GRUB_HIDDEN_TIMEOUT=0默认为0，单系统时启动菜单自动隐藏，要取消自动隐藏菜单，改为大于0再sudoupdate-grub。(注意:单系统下/etc/grub.d/30_os-prober可能没引用这里的变量，如果修改这里不能显示菜单，还要修改/etc/grub.d/30_os-prober，具体看下面修改部份)

GRUB_HIDDEN_TIMEOUT_QUIET=true

GRUB_TIMEOUT="3"----------->设置进入默认启动项的等候时间，默认值10秒，按自己需要修改

GRUB_DISTRIBUTOR=`lsb_release-i-s2>/dev/null||echoDebian`

GRUB_CMDLINE_LINUX_DEFAULT="quietsplash"----------->添加内核启动参数，这个为默认

GRUB_CMDLINE_LINUX="noresume"--------->手动添加内核启动参数，比如acpi=offnoapic等可在这里添加，加text参数启动进入字符模式。


#Uncommenttodisablegraphicalterminal(grub-pconly)
#GRUB_TERMINAL=console---------->设置是否使用图形介面。去除前面#，仅使用控制台终端，不使用图形介面#Theresolutionusedongraphicalterminal
#notethatyoucanuseonlymodeswhichyourgraphiccardsupportsviaVBE
#youcanseetheminrealGRUBwiththecommand'vbeinfo'
#GRUB_GFXMODE=640x480设定图形介面分辨率，如不使用默认，把前面#去掉，把分辨率改为800x600或1024x768
#Uncommentifyoudon'twantGRUBtopass"root=UUID=xxx"parametertoLinux
#GRUB_DISABLE_LINUX_UUID=true---------->设置grub命令是否使用UUID，去掉#，使用root=/dev/sdax而不用root=UUDI=xxx
#Uncommenttodisablegenerationofrecoverymodemenuentrys
#GRUB_DISABLE_LINUX_RECOVERY="true"----------->设定是否创建修复模式菜单项
```

### 2. /etc/grub.d文件夹详细修改方法
再看下/etc/grub.d文件夹下的什么东东：

00_header05_debian_theme10_linux20_memtest86+30_os-prober40_customREADME

前面这五个脚本对应grub.cfg上的各个部分，怎样修改这些脚本文件才能保证不会破坏update-grub的运行，又能让grub.cfg符合你的意愿呢？其实很简单，只要找到

```
cat<<EOF
********
********
********
```

这类语句，EOF中间的文本会直接写入grub.cfg中相应位置，所以个性化的语句添加在这地方就可以了。 00_header可供修改的有两地方

```
cat<<EOF
load_env
setdefault=${GRUB_DEFAULT}<-----这里根据/etc/default/grub中default变量设定，不用修改
if[/${prev_saved_entry}];then
saved_entry=/${prev_saved_entry}
save_envsaved_entry
prev_saved_entry=
save_envprev_saved_entry
insmodjpeg<---------这地方加入要加载的模块，如图片支持，或系统格式支持insmodntfs和insmodfat等
insmodpng<---------
```

另一个在最后

```
cat<<EOF
settimeout=${GRUB_TIMEOUT}<-------timeout根据上面/etc/default/grub中的timeout变量设定，这里不用改
background_image(hd0,7)/boot/images/012.jpg<----------这里背景图片的绝对路径(似乎没有作用，相见"实例"）
05_debian_theme修改背景颜色
cat<<EOF
setmenu_color_normal=white/black<--------
setmenu_color_highlight=yellow/black<-------前面字体颜色可自定，后面背景一定要设为black，不然背景色会挡住背景图片。备注：修改前为setmenu_color_highlight=black/light-gray
10_linux这部分是自动搜索当前系统，建立当前系统的启动菜单，包括系统头，内核等信息，不要随便修改，要使用个性菜单名，比如中文菜单，可修改这里，其余地方不要做修改：
cat<<EOF
menuentry"启动$1"{<---------在双引号""和变量$1这间加入个性文字，或直接把变量$1改为固定字符比如UbuntuKarmic
if["x$3"="xquiet"];then
cat<<EOF
setquiet=1
20_memtest86+添加内存测试启动项，可做修改的地方：
cat<<EOF
menuentry"Memorytest(memtest86+)"{<------可以修改为中文菜单如menuentry"内存测试"｛，双引号必须是英文字符
linux16$MEMTESTPATH
```

### 下面第二个菜单项可删除

```
menuentry"Memorytest(memtest86+)"
linux16$MEMTESTPATH*********
}
30_os-prober查找其他分区中存在的系统并建立菜单项，依次为windows>>linux>>macos，这里不必修改。
或根据自己的系统修改
menuentry"${LONGNAME}(on${DEVICE})"<-------把引号中的变量改为固定，如windowsxp,vista或linux,Fedora之类的菜单项。
40_custom自定义启动项，按菜单标准格式添加即可，update-grub后会自动添加到grub.cfg上，如：
menuentry"启动Veket"{
setroot=(hd0,8)
linux/veket/vmlinuzroot=/dev/ram0PMEDIA=hd
initrd/veket/initrd.gz
menuentry"启动CDLinux"{
setroot=(hd0,8)
linux/CDlinux/bzImageroot=/dev/ram0vga=791CDL_LANG=zh_CN.UTF-8
initrd/CDlinux/initrd
menuentry"启动Grub4Dos"{
setroot=(hd0,8)
linux/grub.exe
```

把各项修改后保存，然后

```
$sudo update-grub
```

### 要修改默认启动项，可以使用下面的方法：
- 1.修改/etc/grub.d/中启动项的顺序，将你想要默认启动的项顺序设置为较小的值。优点是修改不会被update-grub命令覆盖掉，好像没啥缺电，只有另外的程序修改为比你的值更小了才会成为默认启动。
- 2.修改/etc/default/grub中默认的启动项，设置该文件中GRUB_DEFAULT为你想要的值，这个值是生成的grub.cfg中各个启动项的从0开始的下标。该方法优点是修改不会被update-grub命令覆盖，缺点是当启动项的顺序变化之后，下标也就变了。。。

  调整启动画面分辨率

#### 第一步：打开终端，修改/etc/default/grub文件

```
$sudo gedit/etc/default/grub
```

取消#GRUB_GFXMODE=640×480这一行前面的注释符号，并将后面的数字修改为一个合适的值，不需要太高，比如1024x768。这个值同时会影响grub启动菜单和控制台里文字的分辨率。 注意：启动菜单和启动界面分辨率相同，如果此处分辨率设置过高的话，启动菜单会很难看，似乎修改分辨率不会影响启动速度，

#### 第二步：修改/etc/grub.d/00_header文件

```
$sudo gedit/etc/grub.d/00_header
```

按下ctrl+F，查找关键字"setgfxmode=${GRUB_GFXMODE}"(去掉双引号)，然后在这行下面添加新行，内容是："setgfxpayload=keep"(去掉双引号)

#### 第三步：更新grub

```
$sudo update-grub
```

好了，重启试试，不出意外的话你会看到plymouth的启动画面确实更漂亮了

## 给grub2菜单添加图片
### 1.在etc/grub.d文件夹中找到00_header文件，打开后在
save_envprev_saved_entry fi

下添加一句

insmodpng

### 2.在etc/grub.d/05_debian_theme中改为
`setmenu_color_normal=white/black`

> setmenu_color_highlight=yellow/black（前面字体颜色可自定，后面背景一定要设为black，不然背景色会挡住背景图片。前面还有语句的详细）

### 3.根据图片位置可判断系统grub默认图片文件夹位置，在相同位置放上一张同名图片文件即可。
图中文件名为moreblue-orbit-grub.png

#### 一.修改/boot/grub/grub.cfg文件的方法（可以当作修改/etc/grub.d/文件夹和/etc/default/grub文件的参考）
grub.cfg默认为只读，要修改前先设为可写

```
sudochmod+w/boot/grub/grub.cfg
setdefault=0
#默认为0
insmodjpg
#添加jpg支持，如要使用png或tga文件做背景，加上insmodpng或insmodtga(添加图片好像不管用）
insmodext2
#除了用作启动的分区外，其他分区格式可在menu底下再添加
setroot=(hd0,7)
#设定root分区
search-no-floppy-fs-uuid-setf255285a-5ad4-4eb8-93f5-4f767190d3b3
#设定uuid=****的分区为root，和上句重复，可删除
#以下为终端配置
ifloadfont/usr/share/grub/unicode.pf2;then
#设置终端字体，unicode.pf2支持中文显示
setgfxmode=640×480
#设置分辨率，默认为640×480，可用800×600，1024×768，建议跟你想设定的图片大小一致
insmodgfxterm
#插入模块gfxterm，支持中文显示，它还支持24位图像
insmodvbe
#插入vbe模块，GRUB2引入很多模块的东西，要使用它，需要在这里加入
ifterminal_outputgfxterm;thentrue;else
#Forbackwardcompatibilitywithversionsofterminal.modthatdon't
#understandterminal_output
terminalgfxterm
#设置GRUB2终端为gfxterm
settimeout=10
background_image(hd0,7)/boot/images/1.jpg(添加图片好像不管用）
#设置背景图片
###END/etc/grub.d/00_header###
###BEGIN/etc/grub.d/05_debian_theme###
setmenu_color_normal=white/black
setmenu_color_highlight=cyan/black
#这两行为Debian下的菜单颜色设置，如果默认的话，你会发现背景完全被蓝色挡住了，你需要修改blue为black，这样背景就会出现
###END/etc/grub.d/05_debian_theme###
#10_linux为自动添加的当前root分区linux引导项
###BEGIN/etc/grub.d/10_linux###
#菜单项，要包括menuentry双引号""和大括号{}才完整，否则不显示菜单
menuentry"Ubuntu,Linux2.6.31-9-386″{
insmodext2
setroot=(hd0,7)
search-no-floppy-fs-uuid-setf255285a-5ad4-4eb8-93f5-4f767190d3b3
#这句与setroot=(hd0,7)重复，可删除
linux/boot/vmlinuz-2.6.31-9-386root=UUID=f255285a-5ad4-4eb8-93f5-4f767190d3b3roquitesplash
#不喜欢看到一长串的，roo=UUID=***可用root=/dev/sda7代替
initrd/boot/initrd.img-2.6.31-9-386
###END/etc/grub.d/10_linux###
###BEGIN/etc/grub.d/20_memtest86+###
menuentry"Memorytest(memtest86+)"{
linux16/boot/memtest86+.bin
###END/etc/grub.d/20_memtest86+###
#自动添加存在于其他分区的系统引导项
###BEGIN/etc/grub.d/30_os-prober###
#windows启动菜单
menuentry"WindowsVista(loader)(on/dev/sda1)"{
insmodntfs
#windows格式为ntfs，或为fat32改为insmodfat
setroot=(hd0,1)
search-no-floppy-fs-uuid-setece067d2e067a196
#grub2比较先进的地方就是如果发现windows启动是通过ntldr引导的，定为2000/xp/2003，会在这加上drivemap-s(hd0)${root}，作用相当于grub的map，可正常启动非第一硬盘的xp/2003系统。
chainloader+1
#查找到其他分区上的linux系统并自动添加
menuentry"Ubuntukarmic(developmentbranch)(9.10)(on/dev/sda3)"{
insmodext2
setroot=(hd0,3)
search-no-floppy-fs-uuid-set4d893970-0685-44ed-86b3-1de45b2db84a
linux/boot/vmlinuz-2.6.31-9-genericroot=/dev/sda3
initrd/boot/initrd.img-2.6.31-9-generic
}
#若存在macos会自动在这里添加。
###END/etc/grub.d/30_os-prober###
#以下为手动添加的菜单项
###BEGIN/etc/grub.d/40_custom###
menuentry"CDLinux"{
setroot=(hd0,8)
linux/CDlinux/bzImageroot=/dev/ram0vga=791CDL_LANG=zh_CN.UTF-8
initrd/CDlinux/initrd
###END/etc/grub.d/40_custom###
#手动添加时，硬盘编号从0开始(hd0)，主分区编号从1开始(hd0,1)，逻辑分区从5开始(hd0,5)
```

## 二、grub2终端部分命令介绍
在出现选择菜单时，按C进入终端命令行模式，按E进入当前菜单项编辑模式（和grub一样）， 编辑中按Ctrl+C退出，按Ctrl+X以编辑内容启动。

### 1.help
查看命令用法，显示所有可用命令 helpsearch

search命令用法

列出当前的所有设备。如(hd0)(hd0,1)(hd0,5)(hd1)(hd1,1)(hd1,2)....... 详细列出当前的所有设备。对于分区，会显示其label及uuid。

列出当前设为root的分区下的文件

ls(hd1,1)/ 列出(hd1,1)分区下文件

### 3.search
search-f/ntldr 列出根目录里包含ntldr文件的分区，返回为分区号 search-lLINUX 搜索label是LINUX的分区。 search-set-f/ntldr 搜索根目录包含ntldr文件的分区并设为root，注意如果多外分区含有ntldr文件，set失去作用。

### 4.loopback
loopback命令可用于建立回放设备，如 loopbacklo0(hd1,1)/abc.iso 可以使用lo0设备来访问abc.iso里的内容，比如说，可以从abc.iso里的软盘映像中启动 loopbacklo0(hd1,1)/aa.iso linux(lo0)/memdisk initrd(lo0)/abc.img 要删除某一回放设备，可以使用-d参数： loopback-dlo0

### 5.set
使用set可以设置变量的值 setroot= settimeout= 需要调用变量的值时，使用${AA}，如setroot=(hd1,1) 则${root}=(hd1,1)

### 6.pager
分页显示。 setpager=1 满页时暂停，按space继续 setpager=0

### 7.linux
linux取代grub中的kernel

## 三、单linux系统或
硬盘安装时iso放在C盘，umount/isodevice引起的误认为单系统 不能出现菜单项的几种处理方法。

### 1.开机自检后时按几下shift键，可调出菜单项
### 2.sudoupdate-grub
重建grub.cfg，会发现新的系统而改写grub.cfg，一般能出现菜单项

### 3.如第二种方法不能解决，直接修改grub.cfg
把在###BEGIN/etc/grub.d/30_os-prober　中的这一段

```
ifkeystatus;then
ifkeystatus-shift;then
settimeout=-1
settimeout=0
ifsleep$verbose-interruptible3;then
settimeout=0
删除或修改三处settimeout=<大于0>
```

## 四、双硬盘双系统GrubLoading时间过长的解决方案
grub2的boot.img设定root的uuid从第一分区开始搜索分区的/boot/grub下的模块并加载，如果linux分区处于第二硬盘甚至第三硬盘，会导致搜索时间过长而，出现菜单时间会长达10多秒。

对双（多）硬盘的情况建议把grub安装在ubuntu所在硬盘的mbr上，/boot分区或/分区尽量靠前，并设该硬盘为启动盘，会大大缩短启动时间。

## 五、grub2几种修复方法
### 1.双系统重装windows造成grub2被改写的修复
#### 方法一 grub4dos0.4.4
在Windows启动项上加上grub4dos启动（不多说了，看置顶贴），重启选择进入grub，在命令行下输入(/boot单独分区的去掉/boot)

```
grub> find-set-root/boot/grub/core.img
grub> kernel/boot/grub/core.img
grub> boot
```

进入grub2菜单，进入系统后再执行

```
sudogrub-install/dev/sd？
```

#### 方法二 进入Livecd后修复（感谢billbear）
sudo -i mount你的根分区/mnt mount你的/boot分区/mnt/boot#如果有的话

挂载你其他的分区，如果有的话 重建grub到sda的mbr

`grub-install-root-directory=/mnt/dev/sda`

### 2.由于root分区uuid改变造成的不能正常启动，只能进入grubrescue模式的修复

```
grubrescue>set
grubrescue>prefix=(hd？,？)/grub
grubrescue>root=hd？,？
grubrescue>setroot=hd？,？
grubrescue>setprefix=(hd？,？)/boot/grub
grubrescue>set
grubrescue>root=hd？,？
grubrescue>prefix=(hd？,？)/boot/grub
grubrescue>insmod/boot/grub/normal.mod
grubrescue>normal
这时就可以调出/boot/grub/grub.cfg，修改相应uuid，
改到命令行下
grub>insmod/boot/grub/linux.mod
grub>setroot=hd？,？
grub>linux/boot/vmlinuz-***root=/dev/sd？？
grub>initrd/boot/initrg.img-****
hd？,？是grub文件所在分区sda？是/分区。
```

### 3.grub模块和配置文件grub.cfg受损无法启动时修复
Livcd启动进入试用

mount你的根分区/mnt mount你的/boot分区/mnt/boot#如果有的话

挂载你其他的分区，如果有的话 重建grub到sda的mbr

```
grub-install-root-directory=/mnt/dev/sda
```

重建

```
mount -bind /proc/mnt/proc
mount -bind /dev/mnt/dev
mount -bind /sys/mnt/sys
chroot /mntupdate-grub
umount /mnt/sys
umount /mnt/dev
umount /mnt/proc
```

## 六、另一些补充说明
### 1.chainloader
grub2将支持chainloader/file的用法。 目前支持的文件只有grub2的boot.img和grub4dos的grldr和grub.exe。 希望正式版能支持ntldrbootmgrpeldr等文件。

### 2.drivemap
drivemap兼容grub的map，主要用于只能从(hd0)引导启动的系统如win2000xp2003，可以象map用法一样如:

```
menuentry"WindowsXP"{
insmodntfs
drivemap(hd0)(hd1)
drivemap(hd1)(hd0)
setroot=(hd1,1)
chainloader+1
实际上drivemap有了更方便的用法：
menuentry"WindowsXP"{
insmodntfs
setroot=(hd1,1)
drivemap-s(hd0)${root}
chainloader+1
```

### 3.grub2引导软盘img镜像启动
比如要加载(hd1,1)根目录下的a.img镜像，先把memdisk从memdisk.gz中解压出来，用法是:

```
linux(hd1,1)/memdisk#镜像文件超过2.88M要加上c=*h=*s=*
initrd(hd1,1)/a.img
```
