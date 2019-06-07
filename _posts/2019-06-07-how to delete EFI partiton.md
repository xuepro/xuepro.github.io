---
layout:       post
title:         如何删除windows 系统上的EFI系统分区
subtitle:     How to Delete EFI System Partition in Windows 
date:         2019-06-07 07:06:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - DL
---

看这篇文章就行了。
 [How to Delete EFI System Partition in Windows](https://www.easeus.com/partition-master/delete-efi-system-partition.html)
 
Step 1（第一步）. Open DiskPart（打开*DiskPart*）
1. Hit "Windows Key + R" to open the run dialogue box. （点"Windows Key + R" 建 ）
2. Enter diskpart and click "OK" to open a black command prompt window. （命令行窗口输入diskpart）

Step 2. Delete EFI partition with command line （在命令行删除EFI 分区）
Type the below command lines and hit Enter each time（输入下列命令）:

"*list partition*"  (It displays all the volumes on the hard drive.) 
"*select partition 1*" (It identifies which partition you want to remove. Here 1 stands for the volume letter.)
"*delete partition override*" (It removes the EFI partition from Windows disk.) 

如下图所示（我的 EFI系统分区在sidk 1上）：

![](img2/diskpart.png)
