+++
title = "用iptables防止暴力破解ftp密码"
categories = ["原创"]
tags = ["linux"]
date = "2012-05-08 00:00:00"
slug = "yongiptablesfangzhibaolipojieftpmima"
url = "/2012/05/08/e794a8iptablese998b2e6ada2e69ab4e58a9be7a0b4e8a7a3ftpe5af86e7a081/"
draft = false
+++

最近一直有个傻逼黑客暴力破解公司的FTP服务器，虽然我有信心他50年内绝对猜不出密码，但看到日志里一大堆的登录信息还是挺烦的，于是便想用iptables屏蔽它，手工屏蔽肯定是不现实的，人家手上一堆的肉鸡呢，封完一个ip人家换一个ip就行了。解决方法就是写个脚本来分析系统日志，然后识别出属于暴利破解的ip，然后添加到iptables的屏蔽列表中。网上虽然有很多现成的脚本，但都是针对英文系统的，而我公司的系统里面日志是中文的，并不能匹配，只好稍加改变。
show代码：

    #!/bin/bash
    grep "pure-ftpd.*[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}.*WARNING" /var/log/messages | awk '{print $5,$6}' | sed "s/^.*pure-ftpd.*(.*@\(.*\)).*$/\1/g" | sort | uniq -c > /tmp/pureftpban.tmp
    cat /tmp/pureftpban.tmp | while read line
    do
        COUNT1=`echo ${line}|awk '{print $1}'`
        IP1=`echo ${line}|awk '{print $2}'`
        if [ $COUNT1 -gt 10 ] && [ -z "`iptables -vnL INPUT|grep $IP1`" ]
        then
        iptables -I INPUT -s $IP1 -m state --state NEW,RELATED,ESTABLISHED -j DROP
        fi
    done
    
以上代码保存到/root/checksys.sh，并添加可执行权限。
然后用vim编辑/etc/crontab

    vim /etc/crontab
    
添加如下内容：

    */3 * * * * root /root/checksys.sh
    
保存并退出。系统就会每隔3分钟检测是否有人在暴力破解ftp密码，如果次数超过10次，就屏蔽之。
世界终于清静了……