+++
title = "桌面端Firefox远程调试Android端Firefox"
categories = ["原创"]
tags = ["firefox","andorid"]
date = "2014-03-22 00:00:00"
slug = "zhuomianduanFirefoxyuanchengtiaoshiAndroidduanFirefox"
url = "/2014/03/22/firefoxandroidfirefox/"
draft = false
+++

随着智能手机的普及，移动网站的开发也显得也越来越重要了，利用Android版Firefox自带的远程调试功能可以轻松的在PC端调试手机端的网站，实在太方便了。

###具体步骤###

在PC端和手机端都装上Firefox。

PC端Firefox打开about:config，设置devtools.debugger.remote-enabled为True。

手机端Firefox点击菜单栏的"设置"->"开发者工具"，勾选"远程调试"。

![](/static/img/Screenshot_2014-03-22-12-50-24.png)

将手机连接到电脑上，并启用USB调试。

在终端中输入如下命令进行端口转发:

    adb forward tcp:6000 tcp:6000

在PC端Firefox中点击"工具"->"Web开发者"->"连接..."，不用改动它的默认选项，直接点击连接。

![](/static/img/2014-03-22_12.59.39.png)

注意你的手机，应该会出现下图的对话框,点击"确定"即可:

![](/static/img/Screenshot_2014-03-22-13-04-53.png)

现在PC端的Firefox会出现下图:

![](/static/img/2014-03-22_13.07.35.png)

这里就点击"Google"来调试一下Andorid端已经打开的Google网站吧。PC端会弹出一个调试窗口，你可以利用它完全控制Android端Firefox的各种行为。

![](/static/img/2014-03-22-13_20_05.png)

![](/static/img/Screenshot_2014-03-22-13-18-45.png)
