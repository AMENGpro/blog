---
title: "Windows自用设置"
date: 2023-02-02T12:34:56+08:00
draft: false
---

## Windows下载与激活

### ISO下载

* 最好直接下载ISO，而不是通过`创建工具`下载

  * Windows11 https://www.microsoft.com/zh-cn/software-download/windows11

  * Windows10 https://www.microsoft.com/zh-cn/software-download/windows10

{{< admonition type=info title="注意" open=false >}}
对于Windows10的下载页面, 如果浏览器UA是PC, 则只有下载`创建工具`一种方式, 切换为手机UA, 页面就会像Windows11的下载页面一样, 有三种下载方式了。
{{< /admonition >}}

### 激活

适用于Windows10和Windows11

* https://cmwtat.cloudmoe.com/cn.html

### 软件安装前的准备工作
* 更改文档默认位置到D盘

* 安装监控软件[HiBit Uninstaller](https://www.hibitsoft.ir/)

* 安装[IDM](https://www.crackingcity.com/idm-crack/)并注册

  * 修改调用IDM的文件类型：ZIP 7Z RAR EXE ISO MSI

  * 关闭下载浮动条（浏览网页时和选中链接时）

## 软件安装与配置

[QQ音乐](https://y.qq.com/download/download.html)

Office

* [Office4件套](https://otp.landian.vip/zh-cn/download.html)
  * ①部署②安装许可证③安装密钥④设置KMS主机地址⑤激活
  * word关闭智能段落选择：文档-选项-高级-智能段落选择，取消勾选

* [WPS](https://www.wps.cn/)
  * 更改配置，使用脚本自动删除计划任务

* [Adobe Acrobat DC & AI & PS](https://weibo.com/u/1112829033)

娱乐

* [Steam](https://store.steampowered.com/)

* [Steam++](https://steampp.net/)

* Wallpaper Engine

* [TranslucentTB](https://github.com/TranslucentTB/TranslucentTB/releases)

* [QQ游戏](https://qqgame.qq.com/)

* [WeGame](https://www.wegame.com.cn/)

工具

* [VSCode](https://code.visualstudio.com/Download)

* [Git官网](https://git-scm.com/download/win) & [镜像](https://registry.npmmirror.com/binary.html?path=git-for-windows/)

* [IDEA](https://www.jetbrains.com/idea/download/#section=windows)

  * [JAVA](https://www.oracle.com/java/technologies/downloads/)

{{< admonition type=info title="注意" open=false >}}

JAVA安装程序会先安装JDK，然后让你安装JRE。如果你选择JDK和JRE都安装的话，那么你的程序列表中会出现以下两项：

Java 8 Update 361 (64-bit)安装位置：D:\Program Files\Java\jre1.8.0_361

Java SE Development Kit 8 Update 361 (64-bit)安装位置：D:\Program Files\Java\jdk1.8.0_361

前往JDK文件目录下发现有JRE文件夹，与单独安装的JRE文件夹内容基本相同，所以无需单独安装JRE,在安装程序让我们安装JRE时点击右上角关闭即可。

{{< /admonition >}}

* [PyCharm](https://www.jetbrains.com/pycharm/download/#section=windows)

  * [Python](https://www.python.org/downloads/)

* [CLion](https://www.jetbrains.com/clion/download/#section=windows)

  * 自带编译器，如有需求可选其他编译器

* [Fiddler](https://www.telerik.com/fiddler)

* [Postman](https://www.postman.com/downloads/)

* [微信开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)

* [Everything](https://www.voidtools.com/zh-cn/)

* [AIDA64](https://www.aida64.com/downloads)

* [CrystalDiskInfo、CrystalDiskMark](https://crystalmark.info/en/)

[HiBit Uninstaller](https://www.hibitsoft.ir/)

[Clash for Windows](https://github.com/Fndroid/clash_for_windows_pkg/releases/tag/0.20.22)

[QQ](https://im.qq.com/download)

* 设置>会话窗口，关闭消息同步模式
* 删除Q盾组件、停用QQ频道，关闭微信文件自动下载

[微信](https://weixin.qq.com/)

[钉钉](https://page.dingtalk.com/wow/z/dingtalk/simple/ddhomedownload#/)

[腾讯会议](https://meeting.tencent.com/download/)

[百度翻译](https://fanyi.baidu.com/appdownload/download.html?tab=desktop&amp;fr=pcproduct)

[哔哩哔哩直播姬](https://live.bilibili.com/liveHime)

[百度网盘](https://pan.baidu.com/download#win)
* Adobe Acrobat DC、AI、PS、Navicat（AI、PS会自动创建目录，Acrobat DC需手动创建，修改安装路径到"D:\Adobe"）

[阿里云盘](https://www.aliyundrive.com/drive)

[ToDesk](https://www.todesk.com/download.html)

[OBS](https://obsproject.com/)

[7-zip](https://www.7-zip.org/)

[ContexMenuManager](https://gitee.com/BluePointLilac/ContextMenuManager)

[企业微信](https://work.weixin.qq.com/#indexDownload)

## 环境变量

### 系统变量

|变量     |值                       |
|---------|-------------------------|
|JAVA_HOME|D:\Program Files\Java\jdk-1.8|
|~~CLASSPATH~~|~~.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;~~|

{{< admonition type=info title="注意" open=false >}}

* JAVA_HOME这个变量并不是必须要配置的，但是个人建议配置此变量。一是方便引用，用到JDK路径的时候只需要输入%JAVA_HOME%即可；二是当JDK路径改变的时候，只需要修改JAVA_HOME的值即可，否则所有用到JDK路径的地方都需要修改，造成不必要的麻烦；三是有些软件会引用约定好的JAVA_HOME变量，不配置可能会无法正常使用。

* CLASSPATH这个变量我的理解是让Java解释器知道去哪里找类，通过值的内容我们可以知道，“.”表示当前目录，那么首先到当前目录下寻找，找不到的话再去dt.jar（运行环境类库）和tools.jar（工具类库）这两个类库中找。在JDK1.5以后已经不需要再配置CALSSPATH了，根据自己的JDK版本灵活选择。

{{< /admonition >}}

### PATH

{{< admonition type=tip title="技巧" open=true >}}
第一个变量值以`%`开头, 以`;`结束, 比如`%JAVA_HOME%\bin;`, 再次打开`Path`时就会显示为一行, 否则以列表形式显示。
{{< /admonition >}}



## 其他设置

设备名称、鼠标指针、Ctrl显示指针、用户账户控制、高级电源设置

资源管理器设置

浏览器插件设置、搜索引擎

baidu：https://www.baidu.com/s?wd=%s

zhihu：https://www.zhihu.com/search?type=content&q=%s

hanyu：https://hanyu.baidu.com/s?wd=%s&device=pc&from=home

xingce：https://www.fenbi.com/spa/tiku/guide/question/search?q=%s&courseSet=xingce&course=xingce

shenlun：https://www.fenbi.com/spa/tiku/guide/question/search?q=%s&courseSet=shenlun&course=shenlun

huatu：https://v.huatu.com/tiku/searchquestion?keyword=%s

任务计划程序设置（自动删除WPS任务计划程序）

Microsoft-Windows-TaskScheduler/Operational

修改服务为手动或禁用服务：Adobe QQ音乐

工具

系统激活

[制作启动盘](https://www.ventoy.net/cn/download.html)


关闭受限提示
