# 如何选择PHP IDE
大家都是PHP码农精英，个个梦想少花时间写好代码提高效率。使用php集成开发环境可以帮助大家更加容易的实现这个梦想。但是PHP IDE现在五花八门，每一个PHP IDE的官方网站上都鼓吹自己天下第一，弄的哥我眼花缭乱。不知道兄弟你有没有相同的感受，我们一起探讨下如何选择一个好的php集成开发环境。 在本文中，我们挨个深入一下几个最主流的PHP开发工具进行横向评测，希望大家从中找到称手称心的开发工具。

很长一段时间，本人主要开发JAVA,使用Eclipse跟IntelliJ IDEA相当称手。但是自从开发PHP以来，老是找不到好的IDE，于是哥定了8条IDE军规，众观各IDE从容评测之。

## 军规1、语法高亮,增强可读性
## 军规2、自动代码完成及提示
PHP内置类及方法 自定义的类及方法 phpDoc帮助信息提示

## 军规3、代码定位功能，支持方法定义提示及方法使用追踪。
## 军规4、支持突出显示错误与警告
## 军规5、代码自动重构
自动重构在强类型的语言中用的比较多，如Java、C。但是在PHP中也有一点小用。如 当移动文件时，IDE自动修正文件的引用路径 当重命名文件时，IDE自动更新文件的新引用路径 当删除文件时，IDE具备检查引用，并有安全删除的提示 代码格式化

## 军规6、代码自动生成
当类实现接口或抽象类时，可自动生成接口方法或抽象方法 可自动生成getter及setter类似的方法

## 军规7、调试
调试在php中不是很重要，我们通常使用echo或print_r抛出来。但是在大型项目中，过多的"抛出"会污染代码，推荐使用调试。如果IDE足够好，我们可以在调试中查看到变量在每一个程序步骤中的值。

## 军规8、版本控制集成
无论在团队合作还是在个人开发中，好的IDE应该能集成subversion或git，提供直观的文件修改历史、比较、回滚及版本合并。 Web集成

## 军规9、WEB IDE方面支持
在项目中只写php代码不太可能，因为php本身是做web应用的。在现实的php项目中总避免不了与html/css/javascript打交道。能够提供html/css/javascript的支持再好不过

本人用过的几个主流的PHPIDE评测

## 1.PDT 或Zend Studio
Zend Studio是php的官方IDE,不免费，在代码自动完成、生成、提示、调试上功能都很强大。 PDT是ZendStudio的阉割版本，可以参照Zend Studio给出的对比：[http://www.zend.com/products/studio/comparison](http://www.zend.com/products/studio/comparison) 【缺点】 Zend Studio对于html/css/javascript的支持不太好，虽然从Zend Studio9开始Zend Studio已经对html/javascript提供了支持，但是还是功能还是弱些，如css选择器不能自动提示。 【适用者】纯PHP码农，如后端大牛

## 2.Aptana
【优点】 但是Aptana的html/css/javascript支持非常强大，功能齐全，是本人见过最给力的WebIDE。 【缺点】 Aptana 自带的php集成工具并不好用，代码自动提示不完善。尤其自从aptana3以来，强制集成了python跟ruby on rails,运行起来巨吃内存，又慢又肿。

【备注】 本人在前几年一直使用Aptana2+phpeclipse插件+zen coding插件方案，使用phpeclipse的PHP功能，又不失Web方面的支持。 但是phpeclipse长久无更新，Aptana3让人失望至极，本人现在也不用了。 【适用者】纯全模板类码农，如前台开发

## 3.NetBeans PHP
【优点】 跨平台、免费、开放、占用内存小、php及web方法都支持的不错 【缺点】 什么都行什么也不精，php方面跟PDT差不多，不如Zendstudio。WEB方法比Aptana差。 【使用小结】 鸡肋啊鸡肋
