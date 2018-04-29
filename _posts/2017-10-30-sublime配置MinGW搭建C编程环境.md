---
layout:       post
title:        "sublime配置MinGW搭建C/C++编程环境"
subtitle:     "Configure MinGW GCC in Subliem"
date:         2017-10-30 11:06:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - C
---

## sublime配置MinGW搭建C/C++编程环境,并解决控制台汉字输出乱码问题

当安装好MinGW和sublime text后，执行下面2个动作：

1. 按照菜单Tools——>Build System ——>New Build System新建一个“Build System”，其中输出下面内容：

```
{
  "working_dir": "$file_path",
  "cmd": "gcc -Wall -fexec-charset=GBK \"$file_name\" -o \"$file_base_name\"",
  "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
  "selector": "source.c",
 
  "variants": 
  [
    { 
    "name": "Run",
          "shell_cmd": "gcc -Wall -fexec-charset=GBK \"$file\" -o \"$file_base_name\" && start cmd /c \"\"${file_path}/${file_base_name}\" & pause\""
    }
  ]
}
```

将该“Build System”保存为比如“C.sublime-build”到“.../Packages/User/”路径下：Packages/User/C.sublime-build

2. 重启sublime，在Tools——>Build System 选择C


当要编译或运行C程序时，可以“Ctrl + Shift + B”。在弹出菜单中先选择“C”表示编译，然后选择“C-Run”表示运行！

当然如果要编译c++程序，可以将gcc换成g++.
```
{  
  "working_dir": "$file_path",
  "shell_cmd": "g++ -Wall -std=c++14 -fexec-charset=GBK \"$file_name\" -o \"$file_base_name\"",
  "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
  "selector": "source.c, source.c++",
 
  "variants": 
  [
    { 
    "name": "Run",
        "shell_cmd": "g++ -Wall -std=c++14 -fexec-charset=GBK \"$file\" -o \"$file_base_name\" && start cmd /c \"\"${file_path}/${file_base_name}\" & pause\""
    }
  ]
}

```

如果是Linux/Unix系统，需要将cmd换成bash，例如：

```
{
 "cmd": ["g++", "-std=c++14", "${file}", "-o", "${file_path}/${file_base_name}"],
 "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
 "working_dir": "${file_path}",
 "selector": "source.c, source.c++",
 "variants":
 [
   {
     "name": "Run",
     "cmd":["bash", "-c", "g++ -std=c++1y '${file}' -o '${file_path}/${file_base_name}' && '${file_path}/${file_base_name}'"]
   }
 ]
}
```

sublime快捷键：
1. [Rename Variables with Multiple Selection in Sublime Text](https://superuser.com/questions/742438/sublime-text-3-quick-add-find-match-behavior) 

  选择： 变量处双击鼠标；变量前Ctrl cmd G (或Alt F3   Windows/Linux)

  重命名： 变量处双击鼠标；cmd D (或CTRL D  Windows/Linux)
