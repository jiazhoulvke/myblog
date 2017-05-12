+++
title = "vim用的图片热点链接生成工具"
categories = ["原创"]
tags = ["c#","vim"]
date = "2011-05-11 00:00:00"
slug = "vimyongditupianredianlianjieshengchenggongju"
url = "/2011/05/11/vime794a8e79a84e59bbee78987e783ade782b9e993bee68ea5e7949fe68890e5b7a5e585b7/"
draft = false
+++

上次的vim调色板给我很大的启发，利用这种调用图形程序的方式，完全可以将很多原本不能或者很难实现的功能轻易实现，比如这次我需要做一个图片的热点链接（就是在一张图片上划分出N块区域，每块区域都能使用不同的链接），当然不可能还在vim里手工写坐标，那也太逆天了，所以只好无奈的打开N年没用过Dreamweaver，这让我心有不甘，太不装B了！而且Dreamweaver的启动速度也慢得让人蛋疼。这就是我写这个小程序的原因。

本来是想用gtk开发，无奈目前gtk还刚刚入门呢，所以先用我相对比较拿手的C#来开发（开发工具是vs2008 express），等以后再写个gtk版的。

c#的代码比较分散，就不贴上来了，程序和源文件我都打包传到了[我的googlecode](http://jiazhoulvke.googlecode.com)上。直接下载链接：[http://jiazhoulvke.googlecode.com/files/ImageMap%20for%20vim.7z](http://jiazhoulvke.googlecode.com/files/ImageMap%20for%20vim.7z)

下载，解压，复制imagemap.vim到vim的plugin文件夹中，复制imagemap.exe到gvim.exe所在的目录（或者复制到windows系统文件夹下，如c:\windows）,确保已经安装了蛋疼的.net framework（程序用的版本是2.0），在一个空行里输入一个图片名称，必须是有效的，然后在插入模式下按Alt+M(要改快捷键可以到imagemap.vim中改最后一行的代码)，只要图片路径正确，会弹出一个窗口，直接用鼠标拖选一块区域，然后输入链接的属性，就成功添加了一个热点，添加了所有的热点后直接点关闭按钮，生成的代码就出现在vim里了。

下面是截图:

[![](/static/wp-content/uploads/2011/05/11.png)](http://jiazhoulvke.com/?attachment_id=85)

[![](/static/wp-content/uploads/2011/05/2.png)](http://jiazhoulvke.com/?attachment_id=86)

[![](/static/wp-content/uploads/2011/05/3.png)](http://jiazhoulvke.com/?attachment_id=87)

[![](/static/wp-content/uploads/2011/05/4.png)](http://jiazhoulvke.com/?attachment_id=88)
