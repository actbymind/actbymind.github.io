---
layout: post
category : 
tagline: ""
tags : [lua]
---
{% include JB/setup %}

##如何写一个程序
1. 创建一个文本文件，可以为任意后缀，推荐用.lua作为后缀。例如：hello_world.lua

2. 在文件中录入程序代码。例如
hello_world.lua:

        print("hello, world!")

##如何运行一个程序
1. 安装Lua运行环境。linux环境一般默认安装，如果没有安装必须自行安装，在CentOS下可以用命令安装:

        # yum install lua
2. 运行Lua程序。以脚本方式运行:

        $ lua hello_world.lua
        hello, world!
