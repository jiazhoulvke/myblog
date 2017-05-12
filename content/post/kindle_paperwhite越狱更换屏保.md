+++
title = "kindle paperwhite越狱更换屏保"
categories = ["原创"]
tags = ["kindle"]
date = "2013-09-10 00:00:00"
slug = "kindle paperwhiteyueyugenghuanpingbao"
url = "/2013/09/10/kindle-paperwhitee8b68ae78bb1e69bb4e68da2e5b18fe4bf9d/"
draft = false
+++

Kindle paperwhite（以下简称kpw）自带的壁纸其实挺好的，不过看多了也腻，所以想换点新鲜的。不过kpw的壁纸没法自定义，需要越狱以后才能换。

先下载好需要用到的文件：

  * http://s3.amazonaws.com/G7G_FirmwareUpdates_WebDownloads/update_kindle_5.3.5.bin
  * http://www.mobileread.com/forums/attachment.php?attachmentid=103175&d=1363715068
  * http://www.mobileread.com/forums/attachment.php?attachmentid=109554&d=1376755871
  * http://w065855.blob3.ge.tt/streams/3ZRY9XE/combined-dev-certs-20121002.zip?sig=-UEBboFiM5cbpuJPund6fzGi7WxZIkRJqQw&type=download
  * http://www.mobileread.com/forums/attachment.php?attachmentid=110497&d=1378492891

由于版本等于5.3.3或高于5.3.5的系统还无法越狱，我的kpw系统版本是5.3.6,所以要从官方网站上下载5.3.5版的系统进行降级。

将kpw通过usb线连接到电脑上，将update_kindle_5.3.5.bin复制到Kindle的根目录，然后断开usb连接，依次点击菜单按钮(三道杠那个)->"设置"->菜单按钮->"更新您的Kindle"，就开始更新系统了，更新后会自动重启。

再解压下载的那个kpw_jb.zip，里面有这几个文件:

  * jailbreak.mobi
  * jailbreak.sh
  * MOBI8_DEBUG
  * README.txt

连接kpw到电脑，将jailbreak.mobi复制到documents目录中，将jailbreak.sh和MOBI8_DEBUG复制到kpw的根目录，然后断开usb连接，在kpw里就会有本叫《Paperwhite Jailbreak》的书了，点"Jailbreak",然后手指按住左上角的黑点两秒(实际操作中我试了好几次才成功，所以你没成功也不用着急，多按几次)，然后就开始越狱了。

越狱成功后自动重启，会多出来一个jailbreak-log文件，是越狱日志，看看删了就行。

现在可以下载安装最新的5.3.8，越狱不会丢的。不在乎系统新不新的话就保持5.3.5好了，反正也没太大区别。

解压combined-dev-certs-20121002.zip，把其中的update_combined-dev-certs-20121002_install.bin复制到kpw的根目录，断开usb连接，然后像更新系统那样更新就行了。

解压k5_rescure_pack_20130906.zip，将其中的update_rescue_pack.bin复制到kpw的根目录，断开usb连接，然后更新。

解压update_usbnet_0.10.N.zip，复制update_usbnet_0.10.N_install.bin到kpw根目录，更新。

点搜索按钮(也就是那个放大镜)，输入";un"，然后按回车，就开启usbnet模式了(再次输入的话就是关闭)。再次连接电脑，输入如下命令：
    
    sudo ifconfig usb0 192.168.15.1 && ssh root@192.168.15.244

我是直接在~/.bashrc中alias了一个别名：
    
    alias kindle='sudo ifconfig usb0 192.168.15.1 && ssh root@192.168.15.244'

这样每次只要输入kindle就行了。

kpw的root密码为空，提示输入root密码时直接回车即可，然后它会提示你目前系统是只读模式，按照提示输入如下命令进入读写模式：
    
    mntroot rw

[![Screenshot-home-jiazhoulvke.png](/static/wp-content/uploads/2013/09/Screenshot-home-jiazhoulvke.png)](/static/wp-content/uploads/2013/09/Screenshot-home-jiazhoulvke.png)

先将系统原来的屏保备份到kpw的/mnt/us(也就是通过U盘模式连接到电脑上时显示的kpw根目录)：

    mv /usr/share/blanket/screensaver /mnt/us/screensaver.bak

再创建一个软链接，将放置屏保的目录链接到/mnt/us/screensaver：
    
    ln -sfn /mnt/us/screensaver /usr/share/blanket/screensaver

以后要改屏保就直接在电脑上把图片放到kpw的screensaver目录中就行了。

图片要png格式，大小为758x1024，可以通过imagemagick转换，具体怎么转我也就不多说了。

有一点一定要注意！文件名是规定死了的，必须是bg_medium_ss00.png、bg_medium_ss01.png这样的，之前我没改名直接放进去，结果根本没用，Google上搜到的好几篇国人写的教程也都没说，后来看了老外的一篇博文才知道。

文件很多的情况下批量改名很麻烦，所以我写了个小脚本，把这段shell脚本放到screensaver里执行就可以。
    
    #!/bin/bash
    num=0
    for file in ./*.png
    do
        if [ $num -le 9 ];then
            numstr="0$num"
        else
            numstr="$num"
        fi
        mv $file bg_medium_ss$numstr.png
        num=`expr $num + 1`
    done

以后每次添加了新图片后都运行一次就行了。




最后附上高清无码大图一张:




[![IMG_20130910_111300.jpg](/static/wp-content/uploads/2013/09/IMG_20130910_111300.jpg)](/static/wp-content/uploads/2013/09/IMG_20130910_111300.jpg)
