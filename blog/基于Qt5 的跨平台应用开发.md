# 基于Qt5 的跨平台应用开发
<!-- toc -->

- [基于Qt5 的跨平台应用开发](#基于qt5-的跨平台应用开发)
	- [1 Qt简介](#1-qt简介)
	- [2 Qt编程关键技术](#2-qt编程关键技术)
		- [2.1 信号与槽](#21-信号与槽)
		- [2.2 Qt事件处理](#22-qt事件处理)
	- [3. Qt开发与实例分析](#3-qt开发与实例分析)
		- [3.1 开发环境](#31-开发环境)
		- [3.2 系统实现基本框架](#32-系统实现基本框架)
		- [3.3 数据库管理](#33-数据库管理)
		- [3.5 对Excel进行操作](#35-对excel进行操作)
	- [4 系统的打包和测试](#4-系统的打包和测试)
		- [4.1 Mac系统上打包Qt](#41-mac系统上打包qt)
		- [4.2 Windows系统上打包Qt。](#42-windows系统上打包qt)
		- [4.3 发布软件测试](#43-发布软件测试)
	- [5 Qt开发常见问题](#5-qt开发常见问题)
		- [5.1 UI文件转换为头文件问题](#51-ui文件转换为头文件问题)
		- [5.2 Mac打包时出现不包含“libmysqlclient.18.dylib”问题](#52-mac打包时出现不包含libmysqlclient18dylib问题)
		- [5.3 添加应用图标](#53-添加应用图标)
	- [6.参考文献](#6参考文献)

<!-- tocstop -->

## 1 Qt简介
Qt是1991年奇趣科技 开发的一个跨平台的C++图形用户界面应用程序框架。它提供给应用程序开发者建立艺术级的图形用户界面所需的所有功能。Qt很容易扩展，并且允许真正地组 件编程。基本上，Qt 同 X Window 上的 Motif，Openwin，GTK 等图形界 面库和 Windows 平台上的 MFC，OWL，VCL，ATL 是同类型的东西。

2008年，奇趣科技被诺基亚公司收购，QT也因此成为诺基亚旗下的编程语言工具。 2012年，Qt被Digia收购。2014年4月，跨平台集成开发环境Qt Creator 3.1.0正式发布，实现了对于iOS的完全支持，新增WinRT、Beautifier等插件，废弃了无Python接口的GDB调试支持，集成了基于 Clang的C/C++代码模块，并对Android支持做出了调整，至此实现了全面支持iOS、Android、WP。（百度百科）

Qt作为高质量的跨平台框架，具有支持平台广泛、功能完整、开源、执行效率高、界面开发简单、开发工具完备等特性。下表是Qt与目前较为流行的跨平台解决方案Java和Xamarin比较结果。

     | Qt                                | Java                              | Xamarin
:--: | :-------------------------------: | :-------------------------------: | :----------------------------:
桌面平台 | `Windows` `Mac` `Linux` `Solaris` | `Windows` `Mac` `Linux` `Solaris` | `Windows` `Mac` `Linux`
移动平台 | `Android` `iOS` `Window Phone`    | `Android`                         | `Android` `iOS` `Window Phone`
开发语言 | `C++`                             | `Java`                            | `C#`
是否开源 | 有基于LGPL开源版本和商业版本                  | `OpenJDK`开源                       | 有商业版本和基于`Mono`框架为开源
开发工具 | `Qt Creator`  `Qt Designer`       | `Eclipse` `NetBeans`              | `Monodevelop` `Virtual Studio`
功能   | 十分完整                              | 十分完整                              | 不十分完整
开发难度 | 简单                                | 较复杂                               | 较简单
成熟度  | 十分成熟                              | 十分成熟                              | 不十分成熟
版本   | 5..5                              | 8.60                              | 5.7
效率   | 高                                 | 较差                                | 一般
依托公司 | Digia.com(之前为Nokia)               | Oracle.com(之前是SUN)                | Xamarin.com

Qt 不但拥有了完善的C++图形库，而且近年来的版本逐渐集成了数据库、OpenGL库、多媒体库、网络、脚本库、XML库、WebKit库等组件，其核心库 也加入了进程间通信、多线程等模块，极大的丰富了Qt开发大规模复杂跨平台应用程序的能力.Qt的开发工具Qt Creator（IDE）、GUI Designer（界面设计）、Build Tools（编译）、Help System（帮助系统）I18n Tools（多语言工具）等，也极大简化了开发应用的难度。下图为Qt的技术堆栈

![Qt SDK](http://robin.info-lab.top/wp-content/uploads/2016/02/181958415043051.png)

## 2 Qt编程关键技术
### 2.1 信号与槽
信 号和槽机制是QT的核心机制，是一种高级接口，应用于对象之间的通信。信号和槽是QT自行定义的一种通信机制，它独立于标准的C/C++语言，因此要正确 的处理信号和槽，必须借助一个称为 moc（Meta Object Compiler）的Qt工具，该工具是一个C++预处理程序，它为高层次的事件处理自动生成所需要的附加代码。

所有从QObject或 其子类(例如QWidget)派生的类都能够包含信号和槽。当对象改变其状态时，信号就由该对象发射(emit)出去，这就是对象所要做的全部事情，它不 知道另一端是谁在接收这个信号。槽用于接收信号，但它们是普通的对象成员函数。一个槽并不知道是否有任何信号与自己相连接。对象甚至并不了解具体的通信机 制。

信号与槽连接是任意个的，甚至信号与信号也可以连接的，这时无论第一个信号什么时候发射系统都将立刻发射第二个信号。总之，信号与槽构造了一个强大的部件编程机制。

### 2.2 Qt事件处理
Qt可以说是是以事件驱动的UI工具集，信号与槽在多线程的实现也依赖于Qt的事件处理机制。在Qt中，事件被封装成一个个对象，所有的事件均继承自抽象类QEvent。Qt中事件的产生、分发、接受和处理：
- 事件的产生如按键，点击鼠标等等动作所产生的keyPressEvent，  keyReleaseEvent，mousePressEvent，mouseReleaseEvent等事件（分别被封装成QMouseEvent和 QKeyEvent中），这些事件来自于底层的操作系统，它们以异步的形式通知Qt事件处理系统。
- 事件的接受和处理使用QObject。事件处理机制是QObject三大职责（内存管理、内省与事件处理制）之一。任何一个想要接受并处理事件的对象均须继承自QObject，可以选择重载QObject::event()函数或事件的处理权转给父类。
- 事件的分发：对于non-GUI的Qt程序，是由QCoreApplication负责将QEvent分发给QObject的子类-Receiver。对于Qt GUI程序，由QApplication来负责。

## 3. Qt开发与实例分析
下面通过一个指标计算的程序分析Qt开发完整过程。该系统需求：
- 从数据库中读取计算指标参数。（数据库操作组件）
- 计算所的指标需要用温度计的形式展示，并截图以便在文档中使用。
- 能够将计算数据通过Excel导入到数据库中，并能够将计算结果导出到Excel中。
- 需要有Windows和Mac两个版本且功能和界面布局要基本相同。（跨平台）

### 3.1 开发环境
下表为使用的开发环境，基本为开源软件

系统平台   | `Mac OSX 10.11`
:----: | :-------------------------------------------------------------------------:
SDK    | `Qt 5.5`
开发工具   | `Qt Creator` `Qt Designer`
开发语言   | `C++` `SQL`
数据库    | `SQLite 3`
测试平台   | `Mac OSX` `Window XP` `Window 7`
其他开源软件 | `FireFox SQLite Manager` `Inno Setup Compiler` `VirtualBox` `yEd ` `QtXlsx`

### 3.2 系统实现基本框架
该系统综合使用了Qt的数据库模块、GUI模块和第三方的QtXlsx模块，使用VirtualBox完成系统打包和测试，使用Inno setup对Windows程序进行封装，使用SQLite Manager管理SQLite数据库。下图为系统实现基本框架。

![](http://images.cnitblog.com/blog/311130/201411/181958422698949.png)

### 3.3 数据库管理
Qt 对数据的支持相当完善，Oracle、SQL Server、DB2、 SyBase、 MySQL、 PostgreSQL、 SQLite3 都可以完美的支持。由于需求要使用本地数据库并尽可能的小巧灵活，选择SQLite3作为数据库，通过FireFox 插件SQLite Manager进行管理，图4为SQLite Manager 管理界面。Qt使用QsqlDatabase类来管理数据，该类中包括所有数据库的管理行为，如addDatabase为添加数据库驱动，下面为连接 SQLite3示例代码。

```cpp
QSqlDatabase db = QSqlDatabase::addDatabase("QSQLITE");
    if (!QSqlDatabase::drivers().contains("QSQLITE"))
        QMessageBox::critical(0, QObject::tr("Unable to load database"), QObject::tr("This demo needs the SQLITE driver"));
    db.setDatabaseName (dbName);
    if (!db.open()) {
        QMessageBox::critical (0,QObject::tr ("DataBase Error"),db.lastError ().text ());
        return false;
    }
```

数据库连接代码

对于已经连接上的数据库可以使用两种方法来进行操作：
- 1.使用QSqlQuerry，该方法可以直接执行SQL语句，使用与对数据库的批量处理。如：

"query.exec ("DROP VIEW IF EXISTS 'data_x300';");"
- 2.使用QSqlTable，将数据库中的表转换为Qt中的Table，然后进行数据库增添删改等事务性操作，简单而且安全，推荐使用这种方法操作代码。下面为使用QSqlTable代码

```cpp
if((model->insertRow (row))&&
                (model->setData(model->index(row,0),id))&&
                (model->setData(model->index(row,1),name))&&
                (model->setData(model->index(row,2),newPasswd))&&
            (model->setData(model->index(row,3),hint))&&
                (model->submitAll()))
            QMessageBox::warning (this, "Correct","用户添加成功!");
        else
            QMessageBox::warning (this, "Error","密码添加失败!");
```

Qt使用Qt Designer Form，该方法直观且功能强大。首先使用Qt Designer建立并绘制以xxx.ui为后缀的文件，然后在编译时会将其转换为ui_xxx.h头文件，再进行统一的编译。图6为Qt Designer界面。在Qt5加入了对基于JS的QML进行界面的支持，QML觉Qt Designer Form有更强的控制能力和美化能力，而且使用目前流行的JS语言，相信必将成为未来发展趋势。

该系统中还要求用温度计显示计算结果，因此单单是界面绘制工具并不能满足要求。需要先找到温度计的样本图，使用绘图工具进行修改，最后使用Style Sheet脚本对控件进行美化处理。下图为StyleSheet处理脚本和效果。

![](http://images.cnitblog.com/blog/311130/201411/181958498632630.png)

该系统需要对结果截屏，Qt中截屏又两种方式，一种方式是在整个屏幕中，根据相对位置进行截屏（pixmap.grabWindow()）；另外一种是在Qt中的一个窗口中（pixmap.grabWidget()），根据相对位置进行截屏。下面为截屏代码：

```cpp
int grapX= year_lineEdit->geometry ().x ();
int grapY = year_lineEdit->geometry ().y ();
pix = pixmap.grabWidget (this, grapX-2 ,grapY -2, this->width ()-grapX, this->height ()-grapY -140);
```

### 3.5 对Excel进行操作
该系统将需用Excel将计算数据导入到数据库中，并将计算结果导出到Excel中。但在Qt中并没有对Office进行处理的组件，因此需要第三 方组件进行支援。我们使用开源的Qt模块QtXlsx该模块可以对Excel进行操作，功能十分强大。（Qt更多开源模块可以在 [http://inqlude.org](http://inqlude.org) 上找到。）使用方法如下：
- 1.首先在网站上下载QtXlsx模块项目，安装Perl5，使用Qt Creator打开并编译；
- 2.然后再命令行中使用"qmake; make; make install"来安装库
- 3.在pro文件中加入xlsx模块，在头文件中加入"xlsxdocument.h"头文件

即可以使用QtXlsx库进行Excel操作了，下面为QtXlsx操作代码：

```cpp
QString fileName = path + "/index.xlsx";
        QXlsx::Document *xlsx = new QXlsx::Document(fileName);
        int rowC = (model->rowCount ());
        int columnC = (model->columnCount ());
        for (int i = 0; i < columnC; ++i) {
            xlsx->write (1,i+1,model->headerData (i,Qt::Horizontal).toString ());
        }
        for (int i = 0; i < rowC; ++i) {
            for (int j = 0; j < columnC; ++j) {
                xlsx->write ((i+2),(j+1), model->record (i).value (j).toString ());
            }
        }
        if (!fileName.isEmpty()) {
            if(xlsx->save())
                QMessageBox::warning (this,"Correct","数据导出成功");
            else
                QMessageBox::warning (this,"Error","数据导出失败");
        }
```

## 4 系统的打包和测试
### 4.1 Mac系统上打包Qt
需要使用otool和macdeployqt两个工具，otool用于定位适用的动态链接库文件，macdeployqt用于对生成的Release版本的程序进行打包。

具体步骤如下：
- 1.用Qt Creator编译生成Release版本程序，并测试通过；
- 2.进入build-q_-Qt_5_2_1_clang_64-Release文件夹;
- 3.在命令行下使用"otool –L"命令查看适用的动态链接库文件，如图所示。如缺少文件，添加到环境变量中；

![](http://images.cnitblog.com/blog/311130/201411/181958507383729.png) otool输出结果
- 4.在命令行下使用macdeployqt进行打包。下图为打包后应用结构

![](http://images.cnitblog.com/blog/311130/201411/181958523796428.png) 打包应用结构
- 5.生成的App文件再使用Disk Utility程序封装，就可以发布了；

### 4.2 Windows系统上打包Qt。
使用windeployqt工具生成需要打包的文件夹时，会漏掉一些文件，因此需要手动添加一些动态链接库。具体步骤如下：

-1.用VirtualBox 建立Windows 7虚拟机，安装Qt开发完整的平台；
- 2.将QtXlsx源程序拷贝到虚拟机中，安装Perl5，编译安装该模块；
- 3.将待打包应用程序源代码拷贝到虚拟机中，编译成Realse版本应用；
- 4.将应用拷到一个独立文件夹中用windeployqt，生成需要的动态链接库文件；
- 5.将其他需要的动态链接库文件从Qt安装目录中拷贝到该目录中；

![](http://images.cnitblog.com/blog/311130/201411/181958537222983.png) 动态链接文件图
- 6.使用inno setup工具对该目录进行封装即可发布了。

![](http://images.cnitblog.com/blog/311130/201411/181958555977910.png) Inno Setup

### 4.3 发布软件测试
测试采用白盒测试，在Virtual Box分别建立全新的Mac OSX，Windows XP和Windows 7

操作系统虚拟机，将打包程序分别拷贝到相应的系统平台中。分别安装并测试系统功能是否符合要求。如果不符合，需要重新编程、编译、打包和测试，直到满意为止。

## 5 Qt开发常见问题
### 5.1 UI文件转换为头文件问题
有时Qt Creator编译时会出现一些问题，提示缺少ui_**_.h头文件。这是Qt系统出现了问题，解决方法是手动将ui文件转换为相应的头文件。如对_**.ui文件，使用：

```
uic ***.ui -o ui_***.h
```

将其手动的转换为相应的头文件就可以编译了。

### 5.2 Mac打包时出现不包含“libmysqlclient.18.dylib”问题
在Mac系统中打包可能出现缺少"libmysqlclient.18.dylib"文件问题，这是因为系统没有安装MySQL。解决方法是先安 装，macport，然后使用macport安装MySQL。由于默认libmysqlclient.18.dylib文件位置不在搜索目录中，还需要将 其拷贝到相应的目录中。

### 5.3 添加应用图标
对于Windows应用，需要建立一个rc文件说明ico图标文件，在pro文件中添加rc文件。表 为一个示例：

```
#Myapp.rc:
IDI_ICON1              ICON    DISCARDABLE    "myappico.ico"
Myapp.pro:
RC_FILE = myapp.rc
```

对于Mac应用，需要生成图片转成为icns文件，然后在pro文件中添加icns文件：

```
ICON = myapp.icns
```

## 6.参考文献

```
[1] Qt . [EB/OL].http://qt-project.org/

[2] Qt wiki. [EB/OL].http://zh.wikipedia.org/zh-cn/qt

[3] SQLite. [EB/OL].http://sqlite.org/

[4] SQLite Manager . [EB/OL].https://addons.mozilla.org/zh-CN/firefox/addon/sqlite-manager/

[5] GIMP. [EB/OL].http://www.gimp.org/

[6] Inno setup tools. [EB/OL]. http://www.jrsoftware.org/isinfo.php

[7] Virtual Box. [EB/OL]. https://www.virtualbox.org/

[8] OpenOffice. [EB/OL]. http://www.openoffice.org/zh-cn/

[9] yEd. [EB/OL]. http://www.yworks.com/en/products_yed_about.html

[10] QtXlsx. [EB/OL]. http://qtxlsx.debao.me/

[11] Java. [EB/OL]. http://www.java.com/zh_CN/

[12] Xamarin. [EB/OL]. http://xamarin.com/

[13] Mono. [EB/OL]. http://www.mono-project.com/Main_Page

[14] Java. [EB/OL]. http://openjdk.java.net/

[15]Qt 帮助. [EB/OL]. http://qt-project.org/doc/
```

**本文原创，转载请注 [狮子座流星](http://robin.info-lab.top)**
