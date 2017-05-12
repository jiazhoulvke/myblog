+++
title = "linux迁移至固态硬盘全过程"
categories = ["原创"]
tags = ["linux"]
date = "2014-10-27 00:00:00"
slug = "linuxqianyizhigutaiyingpanquanguocheng"
url = "/2014/10/27/linux/"
draft = false
+++

自从台式机上用上固态硬盘后，就再也受不了笔记本上的5400转的机械硬盘了，所以这次又买了块固态硬盘打算装到笔记本上。

笔记本里装的是Ubuntu 14.04 + Win7双系统，Win7主要偶尔运行一些Windows Only的软件，或者偶尔玩一下游戏，没什么特殊的配置，所以重不重装倒无所谓。Ubuntu就不一样了，我的整个开发环境都在里面，假如重装的话配置起来超级麻烦的，当初给台式机重装系统和各种配置就花了我好几天的时间，所以这次决定要直接把原来的系统迁移过来，由于之前没这么干过，整个过程提心吊胆的，还好一次搞定了。

###用到的硬件###

* 笔记本Thinkpad T420，内置日立5400转硬盘、可拆卸式光驱
* 浦科特M6S固态硬盘
* 适用于T420的光驱位硬盘托架
* 容量为4GB的U盘

本次的主角小黑和M6S:

![](/static/img/IMG_20140921_095854.jpg)
　　
![](/static/img/IMG_20141026_160058.jpg)

###具体步骤###

把笔记本自带的机械硬盘拆下来，把固态硬盘换上去；把光驱拆下来，把机械硬盘放到硬盘托里，再把硬盘托放进光驱位。固态硬盘成为主硬盘，机械硬盘成为副硬盘。

将U盘插到电脑上，用Linux自带的dd将ubuntu 14.04的镜像文件写到U盘中:

    sudo dd bs=4M if=/home/jiazhoulvke/Downloads/ubuntu-14.04.1-desktop-amd64.iso of=/dev/sdc

用国产良心软件DiskGenius给固态硬盘分好区:

* 100M的Win7的系统保留分区(有点像Linux里的/boot)。
* 50G的Win7系统分区。
* 8G的Linux交换分区。
* 400M给/boot。
* 剩下的空间全部给/。

安装Win7的过程不在本文讨论范围内，就不详述了。

重启电脑，从U盘启动，进入live系统，挂载分区:

    #sda6为固态硬盘的boot分区
    #sda7为固态硬盘的root分区
    #sdb5为原机械硬盘的windows分区
    #sdb6为原机械硬盘的boot分区
    #sdb7为原机械硬盘的root分区
    sudo -s
    mkdir /mnt/{data,new,old}
    mount /dev/sda7 /mnt/new
    mount /dev/sda6 /mnt/new/boot
    mount /dev/sdb5 /mnt/data
    mount /dev/sdb7 /mnt/old
    mount /dev/sdb6 /mnt/old/boot

用tar备份root分区和boot分区（也可以用dd或者cp -a直接复制，我是顺便做个备份，所以用tar）:

    cd /mnt/old
    tar czf /mnt/data/ubuntu14.04.tar.gz ./*

解压文件到固态硬盘：
    
    cd /mnt/new
    tar xzf /mnt/data/ubuntu14.04.tar.gz

安装grub到固态硬盘:
    
    grub-install /dev/sda
    grub-install --recheck /dev/sda

挂载几个目录:

    mount --bind /proc /mnt/new/proc
    mount --bind /dev /mnt/new/dev
    mount --bind /sys /mnt/new/sys

chroot到固态硬盘的系统中:

    chroot /mnt/new

更新grub配置:

    update-grub

获取新硬盘的各分区的UUID:

    blkid

由于硬盘都已经换了/etc/fstab里的信息肯定也需要更改才行，根据自己的实际情况更改好UUID。

> UUID=825537ad-82f0-44cd-9c3c-fd0603f11576 /               ext4    discard,noatime,errors=remount-ro 0       1 

> UUID=df7e9a69-4f55-45b9-98ef-f5dbf55c72d4 /boot           ext4    discard,noatime,defaults        0       2 

> UUID=02259789-2877-4256-b3d1-4c87e4aa6faa none            swap    sw              0       0 

其中的discard参数是用于开启TRIM功能，noatime参数减少无谓的元数据操作，可延长固态硬盘的使用寿命。

由于8G内存完全够用，所以能不用swap分区就尽量不用。在/etc/sysctl.conf中加入下面这行，减少对swap的使用:

> vm.swappiness=1

现在可以重启体验新硬盘了。

先在win7下用as ssd benchmark测试一下:

![](/static/img/as-ssd-bench PLEXTOR PX-128M6 2014.10.26 19-47-52.png)

写入稍微有点慢，没有台式机上的三星840EVO快，不过还能接受。

![](/static/img/as-ssd-bench Samsung SSD 840  2014.6.11 19-03-57.png)

再在ubuntu下用hdparm对比一下固态硬盘和机械硬盘的速度:

> ~$sudo hdparm -Tt /dev/sda7<br>
> /dev/sda7:<br>
>  Timing cached reads:   13492 MB in  2.00 seconds = 6748.96 MB/sec<br>
>  Timing buffered disk reads: 1276 MB in  3.00 seconds = 424.90 MB/sec<br>
> ~$sudo hdparm -Tt /dev/sdb6<br>
> /dev/sdb6:<br>
>  Timing cached reads:   12904 MB in  2.00 seconds = 6454.72 MB/sec<br>
>  Timing buffered disk reads: 214 MB in  3.02 seconds =  70.76 MB/sec<br>

差距太明显了，原来从开机到进入系统要30秒以上，现在基本上只要10秒左右；原来要好几秒才能启动的程序也基本都是秒开了。如丝般顺滑~~

参考文章:

* https://wiki.archlinux.org/index.php/Solid_State_Drives
