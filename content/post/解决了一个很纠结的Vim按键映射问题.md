+++
title = "解决了一个很纠结的Vim按键映射问题"
categories = ["原创"]
tags = ["vim"]
date = "2011-06-16 00:00:00"
slug = "jiejueliaoyigehenjiujiediVimanjianyingshewenti"
url = "/2011/06/16/e8a7a3e586b3e4ba86e4b880e4b8aae5be88e7baa0e7bb93e79a84vime68c89e994aee698a0e5b084e997aee9a298/"
draft = false
+++

vim里默认的复制粘贴系统剪贴板内容的按键非常的蛋疼，"+y(复制)和"+gP(粘贴)这种按键，光看就觉得别扭，于是一些人就把默认的剪贴板设置为系统剪贴板，有些人则是直接导入vim自带的那个windows按键配置文件，我以前也是一直用这个办法，但很快发现了一个弊端：C-V是用来进入列选择模式的，虽然可以用C-Q代替，但如果使用终端下的vim的话，C-Q通常是不起作用的（在vim输入:h ctrl-Q有解释）。于是我尝试着用&lt;leader&gt;vv这样的组合键来代替C-V，但用了一段时间，连我自己都受不了了，最终还是改回了C-V。然后突然想到，终端里不能按C-Q，那就给它映射个别的按键呗，于是：

    nmap vv <C-Q>

脑袋总算转过弯了……