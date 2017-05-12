+++
title = "windows下配置gtk开发环境(含vim配置)"
categories = ["原创"]
tags = ["dev-cpp","gtk","vim","windows"]
date = "2011-03-30 00:00:00"
slug = "windowsxiapeizhigtkkaifahuanjing(hanvimpeizhi)"
url = "/2011/03/30/windowse4b88be9858de7bdaegtke5bc80e58f91e78eafe5a283e590abvime9858de7bdae/"
draft = false
+++

突然又有了自学C的冲动，决定把遗忘已久的C重新学一遍，不过这次不准备再停留在写些控制台程序的程度，要写一些图形界面的东西了。对我来说，写gui程序当然首选gtk，跨平台，写个程序稍微改一下基本就能在windows和linux下运行了。  

学gtk，用linux是最方便的，可惜由于目前条件所限，已经很久没用心爱的ubuntu了，只好先在windows下将就下了。

Google了一下，发现在windows下想要搭建个gtk的开发环境还真是够复杂的，神马gcc、make、gtk运行库都得自己一个个下载来然后安装配置，而在ubuntu下，一句apt-get命令足矣～

看过好几篇文章，发现[这篇文章](http://justforfun.blog.techweb.com.cn/archives/58.html)(http://justforfun.blog.techweb.com.cn/archives/58.html)里的做法相对来说要简单一些，只需要下载一个dev-cpp和一个gtk for windows的开发包即可。我在很久之前自学C时用的就是dev-cpp，它确实是个很不错的开发工具，非常小巧，只有几M，很适合用来学习，而微软的VS…，几G的体积确实够吓人的，对于初学者来说也完全没必要装这么大个玩意。呃，扯远了，回正题。

按照上面的那篇文章，很快就搭建好了一个gtk开发环境，本来到这一步就可以结束了，但谁叫我是个蛋疼的vim控呢？接下来就配置一下，让vim也能轻松的开发gtk程序。

先修改一下环境变量，把dev-cpp安装目录下的bin目录添加到path环境变量中，比如我的dev-cpp装在c盘根目录，目录的地址是“C:\Dev-Cpp\bin”，这样不需要写完整路径就能在命令行下访问bin目录下的make、gcc程序了。

用vim的基本上都会用taglist这个插件的吧？用taglist的话，基本上都已经装了ctags了（没有的话google下），先在控制台里运行这句命令:

    ctags -R --c++-kinds=+p --fields=+iaS --extra=+q C:\dev-cpp\include

将生成的tags文件改名为c.tags，再运行这句命令:

    ctags -R --c++-kinds=+p --fields=+iaS --extra=+q C:\gtk\include

将生成的tags改名为gtk.tags。然后在vim的安装目录的vim7x(用vim7.2的话x就是2，用vim7.3的话x就是3)目录下新建一个文件夹，名字叫做tagfiles,将之前生成的两个tags文件都复制到这个文件夹下，然后打开_vimrc配置文件，加入以下代码:

    autocmd! BufRead *.c set tags+=$VIMRUNTIME/tagfiles/c.tags,$VIMRUNTIME/tagfiles/gtk.tags

这样编辑c语言文件的时候就可以补全函数了。

接下来写一个简单的gtk文件测试一下。

将以下内容保存为test.c：

    #include <gtk/gtk.h>  
    int main(int argc, char *argv[])  
    {  
        GtkWidget *window;  
        gtk_init(&argc, &argv);  
        window = gtk_window_new(GTK_WINDOW_TOPLEVEL);  
        gtk_window_set_title(GTK_WINDOW(window), “Hello World”);  
        gtk_widget_show(window);  
        gtk_main();  
        return 0 ;  
    }  


再写个makefile:

    gtk_include=-IC:/GTK/INCLUDE/LIBXML2 -IC:/GTK/INCLUDE/LIBGLADE-2.0 -IC:/GTK/LIB/GTKGLEXT-1.0/INCLUDE -IC:/GTK/LIB/GLIB-2.0/INCLUDE -IC:/GTK/LIB/GTK-2.0/INCLUDE -IC:/GTK/INCLUDE/GTKGLEXT-1.0 -IC:/GTK/INCLUDE/ATK-1.0 -IC:/GTK/INCLUDE/CAIRO -IC:/GTK/INCLUDE/PANGO-1.0 -IC:/GTK/INCLUDE/GLIB-2.0 -IC:/GTK/INCLUDE/GTK-2.0 -IC:/GTK/INCLUDE  

    gtk_lib=-LC:/GTK/LIB -lgtk-win32-2.0 -lgdk-win32-2.0 -latk-1.0 -lgdk_pixbuf-2.0 -lpangowin32-1.0 -lgdi32 -lpango-1.0 -lgobject-2.0 -lgmodule-2.0 -lglib-2.0 -lintl -liconv  

    main: test.c  
        gcc -mms-bitfields -Wall -g test.c -o test ${gtk_include} ${gtk_lib}  

    all:  
        ${MAKE} main  


然后在vim执行make，正常的话应该就会生成test.exe文件了。