---
layout: post
category : 
tagline: ""
tags : [git, CentOS]
---
{% include JB/setup %}

##gitolite的用户

    gitolite的使用者可以分为三个部分：
    * gitolite的安装用户
    * gitolite的管理用户
    * gitolite的使用用户
    三个用户可以是一个用户也可以是分开的用户。

##gitolite的安装

1. 安装git

        # yum install git
        # git --version
        git version 1.7.1

2. 创建git用户

        # useradd git -d /home/git

3. 设置管理员

    在管理员下运行

        $ ssk-keygen		#管理帐号
    生成公钥。
    
    拷贝~/.ssh/id_rsa.pub文件。将其放入安装用户git的home目录下命名为admin.pub。
    
    这个公钥可以用于管理员连接服务器时不需要输入密码

4. 安装gitolite

        # su - git
        $ git clone git://github.com/sitaramc/gitolite	#安装帐号
        $ mkdir -p ~/bin
        $ yum install perl-Time-HiRes
        $ gitolite/install -to ~/bin 
        $ gitolite setup -pk admin.pub

##gitolite的使用

1. 安装ssh，并设置开机启动

    ssh服务器默认情况下已经安装，并已经设置开机启动

2. 管理git服务器gitolite

    $ git clone git@the_git_host:gitolite-admin	#管理帐号

    获取来一个gitolite-admin仓库。通过更新这个库管理git服务器

3. gitolite-admin仓库介绍

    gitolite-admin库下面有两个目录：conf和keydir
    keydir目录用于存放所有用户的公钥，名字格式为:用户名.pub
    conf目录下的gitolite.conf用于设置用户访问权限
    gitolite.conf的格式为：

        @用户组                  =   用户1 用户2

        repo 仓库名  
                    权限         =   用户或者用户组  
                    权限2        =   用户或者用户组2 
        repo 仓库名2  
                    权限         =   用户或者用户组  
                    权限2        =   用户或者用户组2 
    权限：
        RW+ 可读写，可push
        RW  可读写
        R   可读
    
4. 添加用户

    将需要接入git服务器的用户的公钥放入gitolite-admin库的keydir目录。
    在gitolite.conf中设置权限

        #管理帐号下执行
        $ git add conf			
        $ git add keydir
        $ git commit -m '**'
        $ git push
    添加用户完毕

5. 添加仓库

    在gitolite.conf加入

        repo 仓库名2  
                    权限         =   用户或者用户组  
                    权限2        =   用户或者用户组2 
