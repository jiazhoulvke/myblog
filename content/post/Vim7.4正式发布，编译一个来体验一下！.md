+++
title = "Vim7.4正式发布，编译一个来体验一下！"
categories = ["原创"]
tags = ["vim"]
date = "2013-08-13 00:00:00"
slug = "Vim7.4zhengshifabu，bianyiyigelaitiyanyixia！"
url = "/2013/08/13/vim7-4e6ada3e5bc8fe58f91e5b883efbc8ce7bc96e8af91e4b880e4b8aae69da5e4bd93e9aa8ce4b880e4b88befbc81/"
draft = false
+++

### 首先安装mercurial

ubuntu/mint的话安装很简单:
    
    sudo apt-get install mercurial

windows的话从这里下载安装: http://mercurial.selenic.com/downloads/

### 下载vim源码

打开shell/cmd,输入:
    
    hg clone https://code.google.com/p/vim/ vim74

### 安装编译工具

ubuntu/mint下可以通过apt-get安装：
    
    sudo apt-get install build-essential xorg-dev libgtk2.0-dev libncurses5-dev python-dev

windows下可以利用[mingw](http://www.mingw.org/)来编译。如果是64位的系统的话可以下载[这个版本](http://jaist.dl.sourceforge.net/project/mingw-w64/mingw-w64/mingw-w64-release/mingw-w64-v2.0.8.tar.gz)。解压后将mingw文件夹中的bin目录加入PATH变量中。

### 开始编译Vim

 * linux

打开shell，cd到vim源码所在目录，执行如下命令:

    ./configure --with-features=huge --enable-fontset  --enable-gui=gtk2 --enable-multibyte --enable-pythoninterp --enable-rubyinterp --enable-sniff --enable-cscope --prefix=/usr

然后:

    make VIMRUMTIME=/usr/share/vim/vim74 && sudo make install

 * windows

打开cmd，cd到vim源码所在目录的src目录中，执行如下命令：
    
    mingw32-make -f Make_ming.mak GUI=yes FEATURES=BIG ARCH=x86-64 OLE=yes STATIC_STDCPLUS=yes PYTHON=D:/bin/Python27 DYNAMIC_PYTHON=yes PYTHON_VER=27 USERNAME=jiazhoulvke USERDOMAIN=gmail.com

有几点需要说明:

  * "ARCH=x86-64"是针对64位系统的，假如你的系统是32位的话请去掉。
  * "PYTHON=D:/bin/Python27 DYNAMIC_PYTHON=yes PYTHON_VER=27"是让vim支持python，请修改"D:/bin/Python27"为你的Python安装路径。假如你不需要对Python的支持，可以去掉这句。

等编译成功后，输入如下命令:

    cd ..
    md vim74
    xcopy runtime\* vim74 /E/Y
    copy src\*.exe vim74
    copy src\GvimExt\gvimext.dll vim74
    copy src\xxd\xxd.exe vim74

创建一个目录,比如D:\bin\vim，把vim74复制过去(假如你已经安装过vim了，请先卸载)。然后运行vim74中的install.exe，输入d后按回车，vim就安装好了。 

### 最后附上我编译的vim74的截图

[![Screenshot-ProjectPath-GVIM.png](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/Screenshot-ProjectPath-GVIM.png)](http://www.jiazhoulvke.com/wp-content/uploads/2013/08/Screenshot-ProjectPath-GVIM.png)

### 嫌自己编译麻烦？

传送门: [http://lilydjwg.is-programmer.com/2013/8/10/vim-7-4-released.40287.html](http://lilydjwg.is-programmer.com/2013/8/10/vim-7-4-released.40287.html)