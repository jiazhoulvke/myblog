+++
title = "树莓派Raspberry Pi与主机进行文件同步"
categories = ["原创"]
tags = ["RaspberryPi","树莓派"]
date = "2013-01-06 00:00:00"
slug = "shumeipaiRaspberry Piyuzhujijinhangwenjiantongbu"
url = "/2013/01/06/198/"
draft = false
+++

### 前言

很想要一个类似于dropbox一样的同步工具来同步主机和树莓派中的文件，很显然树莓派里是别想有dropbox的，所以只好自己动手来实现类似的功能，用到的软件是linux里常见的rsync和python。

### 一、给树莓派设置静态IP

先用ssh登陆到树莓派，给树莓派设置一个静态IP ，可以在路由器上设置，也可以直接在树莓派里设置，我是在树莓派上设置的:
    
    sudo vim /etc/network/interfaces

将内容改成下面这样:

    auto lo
    iface lo inet loopback
    iface eth0 inet static
    address 192.168.1.72
    gateway 192.168.1.1
    netmask 255.255.255.0

保存并退出。

"192.168.1.72"是我给树莓派设置的固定IP，"192.168.1.1"是路由器的IP，请根据你的实际情况进行更改。

重启网络服务:
    
    sudo service networking restart

其实我觉得更方便的办法是直接拔掉电源再重新插上……反正树莓派启动还是挺快的。

现在树莓派的IP变成"192.168.1.72"了。

### 二、设置SSH KEY

为了避免以后每次ssh登陆到树莓派都需要输入密码，可以使用key登陆。

在主机上运行如下命令:
    
    ssh-keygen -t rsa

然后按几次回车，搞定。

接下来用ssh-copy-id把公钥复制到树莓派中:
    
    ssh-copy-id -i  ~/.ssh/id_rsa.pub pi@192.168.1.72

提示让你输入密码，输入密码后回车即可。

之后就可以直接用"ssh pi@192.168.1.72"登陆到树莓派了，不再需要输入密码。

### 三、实现主机到树莓派的同步

分别在主机和树莓派上创建一个文件夹用于同步，先在主机上输入:
    
    mkdir ~/rsync

再在树莓派中输入:
    
    mkdir ~/rsync

再在主机中创建同步脚本:

    vim ~/bin/rsync.py

写入如下内容:
    
    #!/usr/bin/env python
    import gio
    import glib
    import os
    
    RSYNC='/usr/bin/rsync'
    SRC='/home/jiazhoulvke/rsync/'
    DST='pi@192.168.1.72:/home/pi/rsync/'
    
    def directory_changed(monitor,file1,file2,evt_type):
        os.system("%s -ahqzt --delete  %s %s" % (RSYNC,SRC,DST))
    
    gf = gio.File(SRC)
    monitor = gf.monitor_directory(gio.FILE_MONITOR_NONE,None)
    monitor.connect("changed",directory_changed)
    gml = glib.MainLoop()
    gml.run()

其中SRC和DST根据自己的情况进行修改。

赋予脚本可执行权限:
    
    chmod a+x ~/bin/rsync.py

将脚本设置成开机自启动:
    
    sudo vim /etc/rc.local

将下面这行加进去:

    su - jiazhoulvke -c "python /home/jiazhoulvke/bin/rsync.py"

保存退出，然后重启主机。

执行如下命令查看脚本是否正常启动:
    
    ps m|grep rsync.py

假如显示类似如下的内容则表示启动成功:

> 2315 pts/0    -      0:00 python bin/rsync.py

现在测试一下能不能同步，在主机上输入:
    
    touch ~/rsync/test

登陆到树莓派中，输入:
    
    ls ~/rsync

假如看到test文件，说明同步成功，没成功请仔细检查自己是否有哪个步骤做错了。

### 四、实现双向同步

如今从主机到树莓派的单方向同步已经完成了。那么如何让树莓派上的修改也能马上同步到主机呢？很简单，把刚才的所有步骤在树莓派中再做一次，把那个python脚本里的ip地址和用户名都相应改一下就行了，在此就不细说了。

需要注意的是树莓派中的python默认是没有gio这个模块的，得安装一下:
    
    sudo apt-get install python-gobject

另外还要注意自己的主机有没有开启ssh服务，如果没有的话是不能从树莓派同步到主机上的。

PS:unison可以实现双向同步，不过我没试过，反正rsync对我来说已经完全够用了，感兴趣的可以自己尝试。

### 参考资料:

* [http://heylinux.com/archives/817.html](http://heylinux.com/archives/817.html)
* [http://blog.csdn.net/hechaoyuyu/article/details/6384418](http://blog.csdn.net/hechaoyuyu/article/details/6384418)