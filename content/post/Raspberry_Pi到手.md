+++
title = "Raspberry Pi到手"
categories = ["原创"]
tags = ["RaspberryPi","树莓派"]
date = "2012-12-29 00:00:00"
slug = "Raspberry Pidaoshou"
url = "/2012/12/29/189/"
draft = false
+++

Raspberry Pi（国人一般称之为树莓派）最近很火，我受不了诱惑也买了一个来折腾。

[![psb1](/static/wp-content/uploads/2012/12/psb1.jpeg)](http://www.jiazhoulvke.com/?attachment_id=190)

树莓派非常小，显得很可爱。

[![psb2](/static/wp-content/uploads/2012/12/psb2.jpeg)](http://www.jiazhoulvke.com/?attachment_id=191)

旁边的那些板子是用来装树莓派的箱子，是和树莓派一起买来的，那层黄色的纸都可以撕掉的。

[![psb3](/static/wp-content/uploads/2012/12/psb3.jpeg)](http://www.jiazhoulvke.com/?attachment_id=192)

安装很简单，按照说明书用不了多久就可以搞定，最终一个小小的电脑就组装好了。

树莓派除了一块板什么都没有，其他设备都需要另外购买。它用的电源要求电压是5V，电流是750-1000mA，我的手机xt910用的电源是5.1V850mA，正好用得上。它用SD卡来作为存储器，在亚马逊花几十块买了个8G的Sandisk class10 SD卡，在卡上装好raspbian（基于debian的定制发行版），插上网线连上路由器，再插上电源，树莓派成功运行！

树莓派有hdmi接口，可以通过hdmi线输出到支持hdmi的显示器上，或者通过hdmi转vga输出到普通的显示器，不过我并不打算用它来放电影，所以没必要花这冤枉钱了，直接在台式机上通过ssh就能访问树莓派了。在路由器上找到树莓派所使用的ip（也可以在路由器上给它绑定一个静态的IP），通过 ssh pi@ip地址 连接到树莓派，然后输入密码raspberry，即可登陆。

[![Screenshot-pi@raspberrypi: ~-2](/static/wp-content/uploads/2012/12/Screenshot-pi@raspberrypi-2.png)](http://www.jiazhoulvke.com/?attachment_id=193)

登陆后第一步应该是换个更新源，否则默认的源速度会让人发疯的。我目前用的是新加坡的源，有200K以上的速度：

    cat /etc/apt/sources.list
    deb http://mirror.nus.edu.sg/raspbian/raspbian wheezy main contrib non-free rpi

之后就是用更新了：

    sudo apt-get update
    sudo apt-get upgrade

其他的一些配置可以通过一个内置的工具raspi-config搞定：

    sudo raspi-config

[![Screenshot-pi@raspberrypi: ~](/static/wp-content/uploads/2012/12/Screenshot-pi@raspberrypi-.png)](http://www.jiazhoulvke.com/?attachment_id=194)

树莓派的设置基本就搞定了，接下来就是各种折腾了，以后再说……
