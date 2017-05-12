+++
title = "用CrossOver安装Photoshop CS2"
categories = ["原创"]
tags = ["crossover","photoshop","wine"]
date = "2013-08-27 00:00:00"
slug = "yongCrossOveranzhuangPhotoshop CS2"
url = "/2013/08/27/e794a8crossovere5ae89e8a385photoshop-cs2/"
draft = false
+++

### 什么是CrossOver

什么是[crossover](http://www.codeweavers.com/)？用官网[http://www.codeweavers.com/](http://www.codeweavers.com/)上的话说就是“在您的 Linux 操作系统上运行 Windows 软件”，它就是广大Linux群众喜闻乐见的[wine](http://zh.wikipedia.org/wiki/Wine)的商业版，相比wine更易于使用，说白了就是更傻瓜化。

最近crossover正在搞[优惠活动](http://linuxtoy.org/archives/codeweavers-crossover-chinese-official-online-with-sale-activity.html)，原价128块的crossover现在只要64块，和linux有关的付费服务我一直以来是能支持就支持的，只有这样才能促进linux的繁荣嘛，几十块的价格也不算贵，在我能承受的范围，于是果断下单了。炫耀一下软件截图……：

[![crossover.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/crossover.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/crossover.png)

### 获取Photoshop CS2

感谢Adobe大发慈悲，把Photoshop CS2给免费了，让我可以没有负罪感的用它了。b（￣▽￣）d

Photoshop CS2下载地址: [http://download.adobe.com/pub/adobe/magic/creativesuite/CS2_EOL/PHSP/PhSp_CS2_English.exe](http://download.adobe.com/pub/adobe/magic/creativesuite/CS2_EOL/PHSP/PhSp_CS2_English.exe)

因为我的英语是体育老师教的，所以我还要装个汉化包: [http://pcedu.pconline.com.cn/soft/gj/photo/1301/3142835.html](http://pcedu.pconline.com.cn/soft/gj/photo/1301/3142835.html) 。

### 安装Photoshop CS2

这里假设你已经装好了crossover，现在先打开crossover，点击“安装Windows软件”，在弹出的对话框中的“支持的程序”中的第二个就是“Adobe Photoshop CS2”。

[![crossover1.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/crossover1.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/crossover1.png)

选中它，然后点击“选择一个程序安装包”，再点击“选择安装文件”，在弹出的对话框中选择你下载的Photoshop安装文件。

[![crossover2.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/crossover2.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/crossover2.png)

至于下面的容器你可以不用管，没有容器的话crossover会自己创建的。

现在点击“安装”，然后crossover会自动开始从网站上下载所需的运行库及字体，应该会弹出一些对话框，你只要一路点Next就行了。

装完运行库就会开始安装Photoshop了，在要求你输入序列号的时候输入下面这个序列号：
    
> 1045-1412-5685-1654-6343-1431

[![photoshop_setup.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/photoshop_setup.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/photoshop_setup.png)

然后继续一路点Next，安装完成。

接下来就是安装汉化包了。汉化包是一个exe文件，其实就是一个rar自解压程序，直接用unrar就可以解压了：

[![unrar.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/unrar.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/unrar.png)

然后将解压出来的文件全部复制到photoshop安装目录的Required目录中。
    
    cp -v *.dat ~/.cxoffice/Adobe_Photoshop_CS2/drive_c/Program\ Files/Adobe/Adobe\ Photoshop\ CS2/Required

[![hhb.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/hhb.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/hhb.png)

注意到我所写的命令和我实际操作截图里的不同了吗？“Adobe_Photoshop_CS2”是容器名，因为我之前安装了TM2013，所以已经有一个叫“腾讯_TM_2013”的容器了，这次安装Photoshop我选择把它安装到“腾讯_TM_2013”容器里，你如果是新装的容器那名字应该是“Adobe_Photosho_CS2”，请根据你的实际情况操作。

文件复制过去也就安装好了，如果你是安装到新容器的话，100%是会有乱码的，因为crossover官方并没有想到你会安装汉化包，所以默认没有给你安装中文字体，你需要自行安装一个。安装是很简单的，和安装Photoshop的方法几乎一模一样，选择“运行时支持的组件”中的“文鼎中文字体”，然后选择Photoshop所在的容器，点“安装”既可。

[![wending.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/wending.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/wending.png)

按照惯例，又到了秀截图时间了。

[![photoshop.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/photoshop1.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/photoshop1.png)