+++
title = "关于pathogen安装vba包的问题"
categories = ["原创"]
tags = ["vim"]
date = "2012-01-06 00:00:00"
slug = "guanyupathogenanzhuangvbabaodiwenti"
url = "/2012/01/06/e585b3e4ba8epathogene5ae89e8a385vbae58c85e79a84e997aee9a298/"
draft = false
+++

在之前的[一篇文章](http://jiazhoulvke.com/?p=100)中我推荐了几款vim比较实用的插件，其中第一款就是pathogen，是的，虽然只有短短两百来行的代码，但就像我给它的评分一样：Life Changing。

为了解决文件混乱的问题vim搞出了vba这种格式，想法很好，但实际应用中效果却不能尽如人意。因为并非所有的插件发布者都会把插件打包成vba格式，很多都只是简单的压缩成zip或者tar.gz之类的压缩包，假如插件只有一个vim文件的话连压缩都不用了……

而使用pathogen的话，则每个插件都会拥有一个自己的文件夹，这样要删除某个插件直接找到这个插件所在的文件夹，然后删掉它就行了。

好吧，前面说了一大堆废话来凑字数，就是为了引出下面的正题。

现在很多插件都只发布vba包，之前我不知道该怎么解压，用了一种很二的方法：先按照正常的方法安装这个vba包，然后在bundle目录里新建一个目录，再把刚才安装的那些文件移进去……我忘了有伟大的":h"。……

用":h vba"可以看到相关帮助，其实只需要几步就能安装：

1.先创建相应的文件夹。其中的plugin_name是实际的插件名
    
    mkdir ~/.vim/bundle/plugin_name

2.用vim打开需要安装的vba包。
    
    vim someplugin.vba

3.在vim中执行下面的代码:
    
    :UseVimball ~/.vim/bundle/plugin_name

作为一个蛋疼得必须要治的人，我写了小插件，貌似会更方便一点：
    
    "--------------------------------------------------
    " pathogen_install_vba.vim
    " Author:       jiazhoulvke
    " Email:        jiazhoulvke [AT] gmail.com
    " Blog:         http://jiazhoulvke.com
    " Version:      0.1
    "--------------------------------------------------
    
    if &cp; || exists("g:loaded_pathogen_install_vba")
        finish
    endif
    let g:loaded_pathogen_install_vba="v0.1"
    
    command! PathogenInstallVBA :call Pathogen_Install_VBA()
    
    function! Pathogen_Install_VBA()
        let jzlk_extname=expand("%:e")
        if jzlk_extname!="vba"
            echo '这个文件不是vba安装包哦。'
        else
            let vba_dir_name=input("插件文件夹名: ")
            if has("win32")
                let vba_dir_path=$VIM . "\\vimfiles\\bundle\\" . vba_dir_name
                call system("md " . vba_dir_path)
            else
                let vba_dir_path="~/.vim/bundle/" . vba_dir_name
                call system("mkdir ". vba_dir_path)
            endif
            execute 'UseVimball ' . vba_dir_path
        endif
    endfunction
    
安装这个插件，然后以后碰到vba格式的插件，载入后vim里输入:PathogenInstallVBA,会提示输入文件夹名，输入后回车，OK。