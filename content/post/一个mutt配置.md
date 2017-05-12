+++
title = "一个mutt配置"
categories = ["原创"]
tags = ["msmtp","mutt","offlineimap"]
date = "2013-08-15 00:00:00"
slug = "yigemuttpeizhi"
url = "/2013/08/15/e4b880e4b8aamutte9858de7bdae/"
draft = false
+++

mutt的配置挺麻烦的，以前刚学用linux的时候就尝试过一次，失败了，从此再没碰过它，最近再次尝试，发觉也没想象中那么难，这里有我的配置: [mutt_config](https://github.com/jiazhoulvke/mutt_config)，假如你不希望浪费精力去找教程慢慢配置的话，直接用我这个就好了，纯傻瓜式操作（当然也没傻瓜到outlook的地步……）。

mutt与一般的邮件客户端很不一样。像outlook这种客户端，收发邮件和管理邮件都是自己搞定，而mutt则像是个老板，手下有一堆的员工，员工A负责收信，员工B负责发信，mutt只是一个控制中心罢了。我用到的软件(或者说员工)如下：

  * 收信:offlineimap
  * 发信:msmtp
  * 编辑邮件:vim (可以说最吸引我的就是这一点了，用习惯了vim，现在在浏览器里打完一行字都忍不住要按一下ESC……)
  * 邮件提醒:gmail-notify
  * 查看附件:wv、w3m

gmail-notify和offlineimap都被我设为开机自启动，offlineimap在后台隔几分钟同步一次，而当有新邮件时gmail-notify会弹出一个消息框提醒我有邮件。

mutt作为一个纯命令行的邮件客户端自然是没法直接查看html格式的邮件的，所以需要通过w3m将html转换成纯文本；另外对于word、pdf之类的附件，则通过wv这类程序转换后查看;图片也可以调用display来显示。相关的转换规则可以在~/.mailcap里自行定义。

我设置了&lt;super&gt;+M为唤出mutt的快捷键(super是linux下的windows键的叫法)，当我想发邮件或者查看邮件时按一下快捷键马上就能打开，比打开浏览器再点书签或者输网址不知快了多少倍。

[![截图-2013年08月15日-20时36分26秒.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/截图-2013年08月15日-20时36分26秒.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/截图-2013年08月15日-20时36分26秒.png)

目前的使用还比较初级，宏什么的都还没来得及去研究，那才是mutt的精髓所在。

最后秀一下mutt截图：

[![截图-2013年08月15日-20时38分49秒.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/截图-2013年08月15日-20时38分49秒.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/截图-2013年08月15日-20时38分49秒.png)