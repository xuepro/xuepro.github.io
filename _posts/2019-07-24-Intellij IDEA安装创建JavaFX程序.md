---
layout:       post
title:        Intellij IDEA安装创建JavaFX程序
subtitle:     install intellij IDEA and create JavaFX Application
date:         2019-07-24 06:53:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - IT    
---   

### install  intellij IDEA


1. download 

     + **openjdk (jdk12)** at  [http://jdk.java.net/12/](http://jdk.java.net/12/)
     + **javaFX SDK 11**  at [https://gluonhq.com/products/javafx/](https://gluonhq.com/products/javafx/)
     + **intellij IDEA** Community at [https://www.jetbrains.com/idea/download](https://www.jetbrains.com/idea/download)

2. upzip openjdk and javaFX SDK to a directory such as c:\java

3. Configure Environment Variables (Windows)
```
   JAVA_HOME:   c:\java\jdk-12.0.2
   PATH_TO_FX:  c:\java\javafx-sdk-11.0.2
   
   add to system Environment Variable "path": 
         %JAVA_HOME%\bin
```

4. install intellij IDEA 

5. Configure IntelliJ
   
    + Close all open IntelliJ projects to the **Welcome to IntelliJ IDEA** window
    + Go to **Configure** → **Settings** → **Appearance & Behavior** → **Path Variables**
    + Click + to add a **path variable** using:
    
         PATH_TO_FX for the **Name**
         c:\java\jdk-12.0.2 for the **Value**
    +Click OK
    
    + Close all open IntelliJ projects to the **Welcome to IntelliJ IDEA** window
    + Go to **Configure** → **structure for New Project** → **Project setting** → **Project**
    + Click New...
      Select JDK and browse to C:\java\javafx-sdk-11.0.2    
    + Under **Project language level** select **11 - Local variable syntax for lambda parameters**

                或 SDK　　default (12 ,no New language Features)
                
    + Close all open IntelliJ projects to the **Welcome to IntelliJ IDEA** window
    + Go to **Configure** → **structure for New Project** → **Project setting** → **Libraries**
    + Click + ...
      Select C:\java\javafx-sdk-11.0.2  
   


1. 下载安装openjdk (jdk12): http://jdk.java.net/12/
    设置 JAVA_HOM
   将%JAVA_HOME%\bin加到系统路径

2. 安装javaFX SDK 11    不再Swing
  https://gluonhq.com/products/javafx/
  设置 PATH_TO_FX 
   
3. 下载intellij社区版(Community)
   https://www.jetbrains.com/idea/download
   

Reference:

[Installing Java 11](https://taylorial.com/cs1021/Install.htm)

[Getting Started with JavaFX 12](https://openjfx.io/openjfx-docs/#install-javafx)


  
