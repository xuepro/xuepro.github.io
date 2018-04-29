---
layout:       post
title:        "Android Studio 3 教程之3-Scroll Text"
subtitle:     " Android Studio 3 - Scroll Text"
date:         2018-03-08 01:01:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - 安卓
    -  Android
---

视频教程[Android Studio 3.2 安卓开发起步教程](https://ke.qq.com/course/288985?tuin=ac5537fd) 
[Youtube视频网址](​​​​https://www.youtube.com/channel/UCIJLimsCMSfc3wHmevgj8Ng)

## 任务：

Task 1: 添加多个TextViews

Task 2: 添加活动的web links 和 1个ScrollView

Task 3: 滚动(Scroll)多个元素

### 1.1 Create the project 和 TextView 元素

1. creat an App: Scrolling Text

2. Change this view group to RelativeLayout.

3. Add a TextView element above the "Hello World" TextView

```
TextView #1 attribute Value
android:id "@+id/article_heading"
layout_width "match_parent"
layout_height "wrap_content"
android:background "@color/colorPrimary"
android:textColor "@android:color/white"
android:padding "10dp"
android:textAppearance "@android:style/TextAppearance.Large"
android:textStyle "bold"
android:text "Article Title"
```

4. 抽取 **android:text**属性的硬编码字符串"Article Title" 到strings.xml中： **article_title**.

5. 抽取 **android:padding**属性的硬编码"10dp"到dimens.xml，命名为**padding_regular**.

6. 添加另外的TextView元素 在"Hello World" TextView上面，在 刚才的TextView 下面

```
TextView #2 Attribute    Value

android:id    "@+id/article_subheading"
layout_width    "match_parent"
layout_height    "wrap_content"
android:layout_below    "@id/article_heading"
android:padding    "@dimen/padding_regular"
android:textAppearance   "@android:style/TextAppearance"
android:text "Article Subtitle"
```

7. 抽取**android:text**属性的硬编码"Article Subtitle" 命名为**article_subtitle**.

8. 在"Hello World" TextView元素中, 移除 layout_constraint 相关属性.

9. 为 "Hello World" TextView元素添加下列属性并修改android:text属性:

```
TextView Attribute Value
android:id "@+id/article"
android:lineSpacingExtra "5sp"
android:layout_below "@id/article_subheading"
android:text Change to "Article text"
```

10. 抽取"Article text"命名为**article_text**, 抽取"5sp" 为**line_spacing**.

11. 格式化代码 **Code** > Reformat Code**. 


### 1.2 添加文字内容

1. 打开strings.xml.

2. 这是文章标题article_title和子标题 article_subtitle的内容，单行，不能有html标记。

3. 为article_text添加内容.

4.Run the app.


## string.xml

```xml
<resources>
    <string name="app_name">scroll text</string>
    <string name="article_title">滚动文本</string>

    <string name="article_subtitle">子标题</string>

    <string name="article_text">

<b>安卓Android概述</b>
\n\n
Android 是谷歌主导开发的一个开源的、基于 Linux 的移动设备操作系统，如智能手机、平板电脑、穿戴设备、智能电视。
\n\n
Android 应用程序通常借助于Android 软件开发工具如SDK、Android studio集成开发环境，用 Java 语言来编写的。如手机上的支付宝、微博、微信等
\n\n
Android操作系统不断升级，用版本号来区分它们，用甜点的名字来命名它们。如纸杯蛋糕 (Cupcake)、甜甜圈 (Donut)、闪电泡芙 (Eclair)、冻酸奶 (Froyo)、姜饼 (Gingerbread)、蜂巢 (Honeycomb)、冰淇淋三明治 (Ice Cream Sandwich)、果冻豆 (Jelly Bean)、奇巧 (KitKat) 棒棒糖 (Lollipop)、、棉花糖（Marshmallow）、牛轧糖（Nougat）、奧利奧（Oreo）…

<b>Android Studio安装教程</b>：参考 xuepro.xcguan.net.
\n\n

<b>1. 下载安装最新JDK</b>
注意安装目录不能有空格,比如我将按照目录修改为E:\Java\jdk-9。

设置环境变量JAVA_HOME、CLASS_HOME，将jdk安装目录的bin目录添加到系统路径path.

<b><i>JAVA_HOME</i></b>: E:\Java\jdk-9
\n\n
<b><i>CLASS_HOME:</i></b>
\n\n
 .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar
\n\n

<b><i>path: </i></b>
%JAVA_HOME%\bin;%JAVA_HOME%..\jre9\bin
\n\n
\n\n

预览版本下载解压即可，如果是安装程序则运行即可
\n\n
\n
<b>警告:</b>

\n\n
由于总所周知的原因，安装android sdk时几乎不能进行，因为无法访问dl.google.com和ssl-dl.google.com。另外即使安装程序，在实际开发过程中也必须连网同步下载相关组件，所以必须学会“科学上网”！不会科学上网就没法学习Android Studio编程开发！

\n\n
网上许多文章介绍的修改hosts或设置http代理的方法都没法成功安装Android Studio.不要按照这些文章折腾浪费时间了，我浪费了3天时间都没能成功，一般的初始学小白更不行！

\n\n
重要的说3遍：科学上网、科学上网、科学上网！
\n\n
怎么上？问别人或淘宝！
\n\n
另外注意：安装时不要在白天，要在半夜12点后开始下载Android SDK速度才行，白天速度会非常慢！
\n\n
加入QQ群(101132160)，可以直接下载我已经下载好的SDK，这样就不需要等待很长下载SDK了。
\n\n
<b>注:</b>
\n\n
可以解压我下载好的SDK，到默认的SDK位置： C:\Users\username\AppData\Local\Android\sdk
\n\n
其中username是你自己电脑的用户名
\n\n
因为Gradle下载忙，你可以单独下载安装Gradle，过程如下 
</string>

</resources>
```

## activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:paddingBottom="@dimen/activity_vertical_margin"
android:paddingLeft="@dimen/activity_horizontal_margin"
android:paddingRight="@dimen/activity_horizontal_margin"
android:paddingTop="@dimen/activity_vertical_margin"
tools:context="com.example.android.scrollingtext.MainActivity">
<TextView
android:id="@+id/article_heading"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:background="@color/colorPrimary"
android:textColor="@android:color/holo_orange_light"
android:textColorHighlight="@color/colorAccent"
android:padding="10dp"
android:textAppearance="@android:style/TextAppearance.Large"
android:textStyle="bold"
android:text="@string/article_title"/>
<TextView
android:id="@+id/article_subheading"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_below="@id/article_heading"
android:padding="10dp"
android:textAppearance="@android:style/TextAppearance"
android:text="@string/article_subtitle"/>
<TextView
android:id="@+id/article"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_below="@id/article_subheading"
android:lineSpacingExtra="5sp"
android:text="@string/article_text"/>
</RelativeLayout>
```

## Task 2: Add active Web links and a ScrollView

### 2.1 Add the autoLink attribute for active web links

Add the android:autoLink="web" attribute to the article TextView. The XML code for this TextView should now look like
this:

```
<TextView
android:id="@+id/article"
...
android:autoLink="web"
... />
```

### 2.2 Add a ScrollView to the layout

1. 在article_subheading TextView 和the article TextView之间添加1个ScrollView

其android:layout_width和
android:layout_height 属性应该是什么?

2. 删除article TextView的哪个属性？

最后代码应该如下：

```
<TextView
android:id="@+id/article_subheading"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_below="@id/article_heading"
android:padding="10dp"
android:textAppearance="@android:style/TextAppearance"
android:text="@string/article_subtitle"/>
<ScrollView
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_below="@id/article_subheading"></ScrollView>
<TextView
android:id="@+id/article"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_below="@id/article_subheading"
android:lineSpacingExtra="5sp"
android:autoLink="web"
android:text="@string/article_text"/>
```




3. 选择**Code->Reformat Code**格式化代码 

4. Run the app.
滚动文章，注意滚动条的出现，点击web链接访问连接指向的网页. The **android:autoLink**属性使得URL (such as [xuepro.xcguan.net](xuepro.xcguan.net))变成了 web链接.

5. 旋转屏幕，观察滚动效果.

6. 在一个平板或平板模拟器上运行程序，观察滚动效果.

## Task 3: 滚动多个元素

如何使得子标题和文字一起滚动？
