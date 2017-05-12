+++
title = "wine迅雷的乱码问题"
categories = ["原创"]
tags = ["linux","wine","迅雷"]
date = "2013-01-28 00:00:00"
slug = "winexunleidiluanmawenti"
url = "/2013/01/28/winee8bf85e99bb7e79a84e4b9b1e7a081e997aee9a298/"
draft = false
+++

平时下载一些东西我都是直接用浏览器，大一点的会用aria2或者amule，不过对于死链，linux下的所有下载工具都没辙，迅雷在这方面确实是有很大的优势。

我用的是linuxdeepin里提供的打包好的wine迅雷:

> http://packages.linuxdeepin.com/deepin/pool/main/d/deepinwine-thunder5/deepinwine-thunder5_0.0.2_all.deb

顺便提供qq2012和深度截图的地址：

> http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-scrot/deepin-scrot_2.0-0deepin_all.deb  
> http://packages.linuxdeepin.com/deepin/pool/main/d/deepinwine-qq2012/deepinwine-qq2012_0.0.1_i386.deb

wine迅雷下载一般的http资源是一点问题都没有的，速度也很快，但下载bt文件的时候所有的文件名全部是乱码，提示无法保存，让我很无奈，Google了一下，看到[这个帖子](http://forum.ubuntu.org.cn/viewtopic.php?f=121&t=313896)里有人提出同一个问题，原来是要再装一个ie6，这就好办了，打开终端，输入下面的代码：
    
    export WINEPREFIX=$HOME/.deepinwine/wine-thunder5
    winetricks

会出现这样的对话框:

![winetricks](http://www.jiazhoulvke.com/wp-content/uploads/2013/01/Winetricks.png)

点"确定"，再点"Install a Windows DLL or component"，选择"ie6"，点"确定"，然后会弹出提示，让你去 [http://www.oldversion.com/windows/internet-explorer-6-0](http://www.oldversion.com/windows/internet-explorer-6-0) 这个地址下载ie6的安装文件放到_~/.cache/winetricks/ie6_里。

完成后在终端里再次运行_winetricks_，依照之前的顺序点击菜单，就会开始安装了，这一步没啥好说的。

再用wine迅雷打开bt种子，已经不会乱码了。