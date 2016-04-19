# Emacs Basic
<!-- toc -->

- [Emacs Basic](#emacs-basic)
  - [光标移动](#光标移动)
  - [复制、粘贴](#复制-粘贴)
  - [删除](#删除)
  - [查找与替换](#查找与替换)
    - [简单查找替换](#简单查找替换)
    - [正则表达式查找与替换](#正则表达式查找与替换)
    - [正则表达式中的字符：](#正则表达式中的字符)
    - [文本块操作](#文本块操作)
    - [矩形模式](#矩形模式)

  - [Tab 操作](#tab-操作)
  - [Buffer 管理](#buffer-管理)
  - [在C/C++代码中的操作](#在cc代码中的操作)
  - [Emacs中的Register](#emacs中的register)
  - [Save Positions in Registers](#save-positions-in-registers)
  - [Saving Text in Registers](#saving-text-in-registers)
  - [Saving Rectangles in Registers](#saving-rectangles-in-registers)
  - [Saving Window Configurations in Registers](#saving-window-configurations-in-registers)
  - [Keeping Numbers in Registers](#keeping-numbers-in-registers)
  - [Etags](#etags)
  - [Emacs 中的 GNU-Serv](#emacs-中的-gnu-serv)
  - [Emacs中的Bookmark](#emacs中的bookmark)
  - [修改.bashrc，将list-bookmarks绑定到F9上,将bookmark-set绑定到F10](#修改bashrc将list-bookmarks绑定到f9上将bookmark-set绑定到f10)
<!-- tocstop -->

## 光标移动
C-p    向上一行

C-n    向下一行

C-f    向前一个光标

C-b    向后一个光标

M-f    向前一个单词

M-b    向后一个单词

C-a    行首

C-b    行尾

M-a    句首

M-b    句尾

C-v    向下一页

M-v    向上一页

C-M-v    另一个窗口向下一页

C-M-V    另一个窗口向上一页

M-<    文件头

M->    文件尾

C-l    光标位置置于屏幕中间

C-u n 或 M-n  重复执行n次后继命令

## 复制、粘贴
M-w    复制

C-w    剪切/删除

C-y    粘贴

## 删除
C-d    删除光标上的字符

DEL    删除光标前的字符

M-d    删除光标后的单词

M-DEL  删除光标前的单词

C-k    从光标位置删除到行尾

C-S-Backspace  删除当前行

C-y    恢复删除最近的一个

M-y    循环恢复删除上一个

## 查找与替换
### 简单查找替换
C-s    向前递增查找

C-r    反向递增查找

C-s C-w 向前递增查找，把光标所在的单词作为查找对象

C-r C-w 反向递增查找，把光标所在的单词作为查找对象

replace-string  查找替换光标后所有的内容

M-%    查询替换操作

对于M-%，需要注意的是其相关的一些操作：

SPACE或y    用新字符串替换原来的，并进入下一个位置

DEL或n      不替换，进入下一个位置

.          在当前位置做替换后退出查询－替换操作

,          替换，并显示替换情况（再按空格或y进入下一个位置）

!          对后面的内容全部进行替换，不再提问

^          返回上一个替换了的位置

RETURN或q  退出查询替换操作

C-r        进入递归编辑状态

C-w        删除此处内容并进入递归编辑状态（好进行其他修改）

M-C-c      退出递归编辑状态，继续完成查询－替换操作

C-]        退出递归编辑状态和查询替换操作

### 正则表达式查找与替换
C-M-s Return      向前查找正则表达式

C-M-r Return      反向查找正则表达式

C-M-s      向前递归查找正则表达式

C-M-r      反向递归查找正则表达式

query-replace-regexp  查询-替换正则表达式

replace-regexp    无条件替换正则表达式（慎用）

### 正则表达式中的字符：
^          匹配行首

$          匹配行尾

.          匹配任意单个字符

.*        匹配任意个字符

\<        匹配单词的开头

>        匹配单词的结尾

[]        匹配[]中的任何一个字符，如[a-z]匹配任何一个小写字母

### 文本块操作
C-@    标记文本块的开始

C-x C-x 互换插入点和文本标记的位置

M-h    标记整个段落

C-x C-p 标记整个页面

C-x h  标记整个缓冲区

### 矩形模式
Keystrokes            Command name                                            Action

C-x r  k                kill-rectangle                                  Delete a rectangle and store it.

C-x r  d                delete-rectangle                                Delete a rectangle and do not store it.

C-x r  y                yank-rectangle                                  Insert the last rectangle killed

C-x r c                clear-rectangle                                Using spaces, blank out the area marked as a rectangle and do not store it.

C-x r o                open-rectangle                                  Insert a blank rectangle in the area marked.

C-x r r r              copy-rectangle-to-register                  Copy rectangle to register r (where r is any character) .

C-x r i r              insert-register                                Insert rectangle from register r (where r is any character).

（none)                delete-whitespace-rectangle            if a rectangle includes initial whitespace, deletes it, narrowing rectangle.

C-x r t string          Enter string-rectangle                      Change contents of marked rectangle to string (if string is narrower

```
                                                                or wider than rectangle, dimensions change accordingly).
```

(none)                  string-insert-rectangle                    Prompts for string and inserts rectangle.

## Tab 操作
M-[    前一个Tab Group

M-]    后一个Tab Group

M-p    前一个Tab

M-n    后一个Tab

## Buffer 管理
C-x C-b    进入buffer管理窗口

## 在C/C++代码中的操作
M-a    移动到当前语句的开始

M-e    移动到当前语句的末尾

C-M-a  移动到当前函数的开始

C-M-e  移动到当前函数的结尾

M-q    若光标在注释文本中间，则进行段落重排，保留缩进和前导字符

C-M-h  把光标放在当前函数开头，把文本块标记放在函数结尾，

```
    即把函数整个选作为一个文本块。
```

C-c C-q 对整个函数进行缩进

C-x h  选定整个buffer，  然后C-M-\可以对代码进行重新排版

C-c C-u 移动到当前预处理条件的开始位置

C-c C-p 移动到上一个预处理条件

C-c C-n 移动到下一个预处理条件

M-;    对当前行进行注释

C-x C-x 快速返回移动前的光标位置

C-c C-c 对一块代码进行注释；取消注释用命令 uncomment-region

## Emacs中的Register
Emacs中的register

在多个文件中逛的时候，我们常常需要快速切换到先前访问的某个位置。因此，我们需要把文件及其光标位置暂时存放在某个地方。

在Emacs中，我们可以使用register暂时性保存这些信息。

将当前光标所在位置保存入一个register中：

C-x r SPACE + register名（一个字符，比如a吧）

然后我们就可以到处瞎逛，若要回到保存的register a位置，我们可以输入：

C-x r j a

挺好用的吧:)

如果你记性和我一样不好，恐怕会常常想看看自己保存了哪些register，我们可以输入：

M-x view-register    查看某一个register

M-x list-registers  查看所有的register

其实我常用的就是以上功能，为了使笔记稍微完整一点，下面开始Copy 《GNU Emacs Manual》的相关章节：

在下面，我们使用r来命名所有的register：

## Save Positions in Registers
C-x r SPC r

```
Save position of point in register r (point-to-register).
```

C-x r j r

```
Jump to the position saved in register r (jump-to-register).
```

## Saving Text in Registers
C-x r s r

```
Copy region into register r (copy-to-register).
```

C-x r i r

```
Insert text from register r (insert-register).
```

M-x append-to-register RET r

```
Append region to text in register r.
```

M-x prepend-to-register RET r

```
Prepend region to text in register r.
```

## Saving Rectangles in Registers
C-x r r r

```
Copy the region-rectangle into register r (copy-rectangle-to-register). With numeric argument, delete it as well.
```

C-x r i r

```
Insert the rectangle stored in register r (if it contains a rectangle) (insert-register).
```

## Saving Window Configurations in Registers
C-x r w r

```
Save the state of the selected frame's windows in register r (window-configuration-to-register).
```

C-x r f r

```
Save the state of all frames, including all their windows, in register r (frame-configuration-to-register).
```

## Keeping Numbers in Registers
C-u number C-x r n r

```
Store number into register r (number-to-register).
```

C-u number C-x r + r

```
Increment the number in register r by number (increment-register).
```

C-x r g r

```
Insert the number from register r into the buffer.
```

## Etags
建立Etags文件：

在代码目录中运行etags -R

如果要向现有tags表中添加，则运行etags -a

访问Tag文件：

M-x visit-tags-table

常用热键

M-.      访问tag

C-u M-.  访问下一个tag

M-*      返回

## Emacs 中的 GNU-Serv
常常使用console的人往往也改不了这么个习惯，就是进了X就开个终端，然后在里头埋头干活，看到什么文件想修改就vi一把。我也是这个习惯。vi比emacs启动快多了。

GNU-Serv改变了这个情形。

首先要安装gnu-serv这个包，在我的机器上apt-get install gnu-serv就可以了。

接下来修改.emacs文件

(require 'gnuserv)

(gnuserv-start)

接下来修改.bashrc文件

alias e='gnuclient'

这样，在终端下就可以通过 e foo来编辑foo文件了，它会自动关联到已经打开的emacs中。

更强大的功能在于，你还可以在远程执行gnuclinet，在本机编辑文件后自动存放到远程机器上。

## Emacs中的Bookmark
Emacs中的bookmark

将当前页面加入bookmark

M-x bookmark-set

## 修改.bashrc，将list-bookmarks绑定到F9上,将bookmark-set绑定到F10
(global-set-key [(f9)] 'list-bookmarks)

(global-set-key [(f10)] 'bookmark-set)

这样，就可以通过F9键访问书签,通过F10将当前页添加为书签了

Emacs 配置的一些tips

在GBK环境下配置Emacs使之可以阅读UTF-8文档

其实可以给 utf-8 优先级：

(prefer-coding-system 'utf-8)

HTML generated by org-mode TAG=7.01g in emacs 23
