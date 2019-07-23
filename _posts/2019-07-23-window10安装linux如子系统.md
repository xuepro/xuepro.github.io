---
layout:       post
title:        window10安装linux如子系统
subtitle:     Window 10 install linux ubuntu subsystem 
date:         2019-07-23 09:36:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - IT    
---   

           window10   安装  linux(ubuntu)子系统
                       http://hwdong.net

1. 设置->更新与安全->开发者选项->勾选"开发人员模式"

![](https://upload-images.jianshu.io/upload_images/11697950-6af29dfda4544307.png)

2. 设置->应用->应用和功能->程序和功能->启用或关闭windows功能
             ->勾选“适用于Linux的Windows子系统”

windows系统->控制面板->程序->程序和功能->启用或关闭windows功能
             ->勾选“适用于Linux的Windows子系统”
             
![](https://upload-images.jianshu.io/upload_images/11697950-b1f8fa3b7136ae89.png)

![](https://upload-images.jianshu.io/upload_images/11697950-9376e1900c331697.png)

3. 系统重启后
   底部搜索放大镜->搜索“商店”或"store"，打开“微软应用商店”，
   搜索“ubuntu”，点“安装”
   设置你的  用户名 和 密码

4. “开始”菜单打开“ubuntu”`进入

    ls    
    
    sudo +命令： sudo apt update   sudo apt upgrade 
    
    退出：CTRL+D  exit  logout
