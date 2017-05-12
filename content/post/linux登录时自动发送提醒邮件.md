+++
title = "linux登录时自动发送提醒邮件"
categories = ["原创"]
tags = ["linux","sendmail"]
date = "2013-08-04 00:00:00"
slug = "linuxdenglushizidongfasongtixingyoujian"
url = "/2013/08/04/linuxe799bbe5bd95e697b6e887aae58aa8e58f91e98081e68f90e98692e982aee4bbb6/"
draft = false
+++

最近黑客太猖獗了，看公司的服务器日志文件可以看到每天黑客尝试各种sql注入各种扫描，于是我希望有一天当服务器真被攻破时，有用户通过ssh登录到公司的服务器后我能及时收到邮件提醒。

由于用户在登录时都会读取/etc/bashrc这个文件，利用这个原理，只要把shell脚本写在里面就会自动执行了。

最开始的版本是这样的:
    
    EMAILTMPFILE='/tmp/.userlogin.tmp'
    echo "From: root@wtf.com" > $EMAILTMPFILE
    echo "sender: root@wtf.com >> $EMAILTMPFILE
    echo "To: jiazhoulvke@鸡妹儿.com" >> $EMAILTMPFILE
    echo "Subject: `whoami`登录到服务器" >> $EMAILTMPFILE
    echo "" >> $EMAILTMPFILE
    echo "时间:`date '+%Y-%m-%d %H:%M:%S'` >> $EMAILTMPFILE
    (cat $EMAILTMPFILE | sendmail jiazhoulvke@鸡妹儿.com && rm -f $EMAILTMPFILE) &

gmail可以正常接收，并且不会乱码。但当我把邮件通过gmail转发到139邮箱时(因为139邮箱有免费的短信提醒)，在139邮箱里会乱码。

这时就需要设置邮件的编码，邮件内容可以通过添加一个邮件头来说明它的编码，在Subject这行上面加入"Content-type: text/html;charset=utf-8"就行了。

邮件标题就有点麻烦了，得先用base64编码，然后在前后分别加入"=?UTF-8?B?"和"?="才行。也就是：
    
    Subject: =?UTF-8?B?已进行base64编码的标题?=

最后我想知道到底当前有那些登录用户，他们的IP是什么，于是利用w命令来输出这些内容:

    w | sed "s/$/<br\/>/g" | sed "s/\ /\&nbsp;/g" >> $EMAILTMPFILE

所以最终的版本如下：
    
    EMAILTMPFILE='/tmp/.userlogin.tmp'
    echo "From: root@wtf.com" > $EMAILTMPFILE
    echo "sender: root@wtf.com >> $EMAILTMPFILE
    echo "To: jiazhoulvke@鸡妹儿.com" >> $EMAILTMPFILE
    echo "Content-type: text/html;charset=utf-8"
    MAILSUBJECT="`whoami`登录到服务器"
    MAILSUBJECT_BASE64=`echo $MAILSUBJECT | base64`
    echo "Subject: =?UTF-8?B?$MAILSUBJECT_BASE64?=" >> $EMAILTMPFILE
    echo "" >> $EMAILTMPFILE
    echo "时间:`date '+%Y-%m-%d %H:%M:%S'` >> $EMAILTMPFILE
    w | sed "s/$/<br\/>/g" | sed "s/\ /\&nbsp;/g" >> $EMAILTMPFILE
    (cat $EMAILTMPFILE | sendmail jiazhoulvke@鸡妹儿.com && rm -f $EMAILTMPFILE) &

下辈子再也不想搞和网站有关的东西了，真心苦逼。