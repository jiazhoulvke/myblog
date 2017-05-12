+++
title = "vim里的调色板"
categories = ["原创"]
tags = ["gtk","vim"]
date = "2011-04-09 00:00:00"
slug = "vimliditiaoseban"
url = "/2011/04/09/vime9878ce79a84e8b083e889b2e69dbf/"
draft = false
+++

今天无意中看到了一篇文章《[colorpicker: 给 Vim 加一个调色板！](http://lilydjwg.is-programmer.com/posts/21636.html)》，才知道原来vim里也能调用调色板，唉，火星了。

colorpicker需要一段vim代码和一个gtk程序的配合，作者给出了gtk程序的代码，但没有windows下的可执行程序，正好我前不久刚刚搭建了一个windows下的gtk开发环境，于是就派上用场啦。写了一个makefile，一次性编译通过，嘿嘿！

文件下载地址:
googlecode:[http://jiazhoulvke.googlecode.com/files/colorpicker_for_vim.7z](http://jiazhoulvke.googlecode.com/files/colorpicker_for_vim.7z)

压缩包下载下来后，解压，将plugin文件夹里的colorpicker.vim复制到vim里的相应目录中，再把colorpicker文件夹中的colorpicker.exe复制到系统目录中，比如c:\windows。不过我比较喜欢把程序放到vim的安装目录里面，比如c:\program files\vim\vim73，vim一样可以访问到，而且更加绿色环保。

现在一切搞定了，打开vim，按Alt+C，就会弹出一个调色板了，hoho～～

[![](http://jiazhoulvke.com/wp-content/uploads/2011/04/colorpicker.jpg)](http://jiazhoulvke.com/?attachment_id=71)

update:回去看了一下依云同学（colorpicker作者）博客的更新，才想起用windows的人基本都没装过gtk运行库的，失策啊，没这玩意是用不了colorpicker，赶紧的，去下载个gtk运行库吧！[http://gtk-win.sourceforge.net](http://gtk-win.sourceforge.net)