+++
title = "让windows下的vim支持vimpress"
categories = ["原创"]
tags = ["python","vim"]
date = "2011-03-01 00:00:00"
slug = "rangwindowsxiadivimzhichivimpress"
url = "/2011/03/01/e8aea9windowse4b88be79a84vime694afe68c81vimpress/"
draft = false
+++

由于wordpress总会很“贴心”的删掉我贴的代码里的空格(还好我贴的是vimscript和javascript，不讲究缩进，如果贴的是python，那不是要抓狂了么？)，所以我一直在找一个比较好用又不会自作聪明的离线编辑器。

微软的客户端蛋疼的不支持Windows2003，其他的一些离线编辑器感觉也不怎么好用，最终还是选择了[vimrepress](http://wowubuntu.com/vimrepress.html)，依赖python。我用的vim版本是7.2，默认支持的python版本是2.4，有点太低了，所以，还是得重新编译一个vim，让它支持更新版本的python。由于网上已经有人编译了支持python2.5和2.6的vim，所以不需要我们再去编译了，网址:[http://www.gooli.org/blog/gvim-72-with-python-2526-support-windows-binaries/](http://www.gooli.org/blog/gvim-72-with-python-2526-support-windows-binaries/)。里面有两个压缩包，一个是支持python2.5,一个是支持2.6，除非有特殊要求，否则一般来说当然是新的更好，所以我下载了gvim72python26.zip这个文件。

下载后解压会得到两个文件：gvim.exe和vim.exe，用这两个文件覆盖vim安装目录下的同名文件即可。

然后从python的官方网站上下载python2.6并安装，并把python的安装路径添加到系统环境变量里面，一切大功告成！

顺便说句，这篇文章就是在vimrepress里写的，嘿嘿！