---
layout:       post
title:        "Android Studio 3 教程之1-Hello World程序"
subtitle:     "Android studio - hello world program"
date:         2018-03-03 11:30:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - 安卓
---

注意：文章中的部分图片或网址需科学上网才能看到！

附：[Android Studio 3.2 教程1-HelloWorld](http://www.365yg.com/item/6538692836705960462/)

视频教程[Android Studio 3.2 安卓开发起步教程](https://ke.qq.com/course/288985?tuin=ac5537fd) 
[Youtube视频网址](​​​​https://www.youtube.com/channel/UCIJLimsCMSfc3wHmevgj8Ng)

## 安卓Android概述
Android 是谷歌主导开发的一个开源的、基于 Linux 的移动设备操作系统，如智能手机、平板电脑、穿戴设备、智能电视。

Android 应用程序通常借助于Android 软件开发工具如SDK、Android studio集成开发环境，用 Java 语言来编写的。如手机上的支付宝、微博、微信等


Android操作系统不断升级，用版本号来区分它们，用甜点的名字来命名它们。如纸杯蛋糕 (Cupcake)、甜甜圈 (Donut)、闪电泡芙 (Eclair)、冻酸奶 (Froyo)、姜饼 (Gingerbread)、蜂巢 (Honeycomb)、冰淇淋三明治 (Ice Cream Sandwich)、果冻豆 (Jelly Bean)、奇巧 (KitKat)
棒棒糖 (Lollipop)、、棉花糖（Marshmallow）、牛轧糖（Nougat）、奧利奧（Oreo）...


![](https://wx2.sinaimg.cn/mw690/006Lkwkygy1fozidmc1z3j30q10gmaf7.jpg)


Android提供给程序员用来开发应用程序的库API也不断升级，也用不同的API版本号来区分它们。


## Android 软件架构

![](http://www.runoob.com/wp-content/uploads/2015/06/android_architecture.jpg)


## 安装最新版 Android Studio


#### 1.  下载安装最新[JDK](http://www.oracle.com/technetwork/java/javase/downloads/)
![](http://www.oracle.com/ocom/groups/public/@otn/documents/digitalasset/1612441.gif)

注意安装目录不能有空格,比如我将按照目录修改为E:\Java\jdk-9。

设置环境变量JAVA_HOME、CLASS_HOME，将jdk安装目录的bin目录添加到系统路径path.

**JAVA_HOME:** E:\Java\jdk-9

**CLASS_HOME:** .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar

**path**:  %JAVA_HOME%\bin;%JAVA_HOME%\..\jre9\bin



#### 2. 下载安装最新[Android Studio 3.2](https://developer.android.com/studio/preview/index.html)

![](https://cdn57.androidauthority.net/wp-content/uploads/2017/05/android-studio-logo-840x359.png)

预览版本下载解压即可，如果是安装程序则运行即可


**警告**:  

由于总所周知的原因，安装android sdk时几乎不能进行，因为无法访问dl.google.com和ssl-dl.google.com。另外即使安装程序，在实际开发过程中也必须连网同步下载相关组件，所以必须学会“**科学上网**”！不会科学上网就没法学习Android Studio编程开发！

网上许多文章介绍的修改hosts或设置http代理的方法都没法成功安装Android Studio.不要按照这些文章折腾浪费时间了，我浪费了3天时间都没能成功，一般的初始学小白更不行！

重要的说3遍：科学上网、科学上网、科学上网！

怎么上？问别人或淘宝！

另外注意：安装时不要在白天，要在半夜12点后开始下载Android SDK速度才行，白天速度会非常慢！

加入QQ群(101132160)，可以直接下载我已经下载好的SDK，这样就不需要等待很长下载SDK了。

**注:**

* 可以解压我下载好的SDK，到默认的SDK位置：
    C:\Users\username\AppData\Local\Android\sdk

    其中username是你自己电脑的用户名

* 因为Gradle下载忙，你可以单独下载安装Gradle，过程如下

```
  1) 在[https://gradle.org/releases/](https://gradle.org/releases/)下载Gradle（如 gradle-4.5-all.zip）

  2) 将Gradle-×-×.zip解压到,并拷贝到位置：

  C:\Users\{USERNAME}\.gradle\wrapper\dists\

  或者也可以这样：

  2) 打开Android Studio : File > Settings > Gradle > Use local gradle distribution指定你的Gradle目录位置，点击apply 和 ok

```

[Manually install Gradle and use it in Android Studio](https://stackoverflow.com/questions/26254526/manually-install-gradle-and-use-it-in-android-studio)

* Gradle离线工作，Settings -> Build, Execution, Deployment -> Build tools -> Gradle勾选"offline work"

另可以参考[加速Android Studio的Gradle构建速度](https://www.jianshu.com/p/2a58fd896214)

## 3. hello world程序

#### 创建hello world 工程：

"Start a new Android Studio project".

![](https://developer.android.com/training/basics/firstapp/images/studio-welcome_2x.png)

在弹出的“Create New Project”窗口,为你工程起一个名字如"My First App"，一路next就可以了.

#### 首次使用检查JDK的路径：

在File > Project Structure > [Platform Settings] > SDKs 修改JDK为你的JDK目录

#### 运行run你的程序：

有2种运行方式：物理设备或虚拟设备上运行。

1) 点击"Project"窗口中的"app"模块,选择菜单“ Run > Run”或工具栏的Run图标 ![](https://developer.android.com/studio/images/buttons/toolbar-run.png)

2)在“Select Deployment Target”窗口,选择你的物理设备（假如你插入了你的手机）或虚拟设备。


a)选择物理设备 :确保手机连上电脑，手机的调试模式开启！

![](https://developer.android.com/training/basics/firstapp/images/run-device_2x.png)

b)创建一个虚拟设备"Creat New Virtual Devide"，创建虚拟设备过程中会下载相关的组件/库。创建虚拟设备时会下载相应的API库、下载安装intel HAXM等。可能需要修改你自己电脑的BIOS开启虚拟化技术！

![](https://cdn57.androidauthority.net/wp-content/uploads/2017/05/Select-Hardware-840x665.png)

你可以创建多个不同的虚拟设备，选择1个虚拟设备！


注：

* 电脑的内存至少8G,建议16G. 否则Android Studio编译会很慢。

* 关于该hello world程序的更多解释，如目录结构、界面布局UI、资源等请观看视频课程！



参考：

[https://developer.android.com/studio/preview/install-preview.html](https://developer.android.com/studio/preview/install-preview.html)

[https://developer.android.com/training/basics/firstapp/running-app.html](https://developer.android.com/training/basics/firstapp/running-app.html)

[Android Hello World 实例](http://www.runoob.com/android/android-hello-world-example.html)

[https://www.androidauthority.com/android-studio-tutorial-beginners-637572/](https://www.androidauthority.com/android-studio-tutorial-beginners-637572/)