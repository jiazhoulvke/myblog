+++
title = "我的项目管理插件myproject"
categories = ["原创"]
tags = ["myproject","plugin","vim"]
date = "2012-06-28 00:00:00"
slug = "wodixiangmuguanlichajianmyproject"
url = "/2012/06/28/e68891e79a84e9a1b9e79baee7aea1e79086e68f92e4bbb6myproject/"
draft = false
+++

发个我自己写的项目管理插件myproject，目前实现了针对项目手动/自动更新tags及cscope数据库、在项目中递归搜索等功能，自己用着还挺舒服的。  

项目地址:[https://github.com/jiazhoulvke/myproject](https://github.com/jiazhoulvke/myproject)  

最开始的版本是纯vimscript的，受不了更新tags时老是弹出命令行窗口，所以改成了python的，用vim的应该都装了python，所以应该不算什么大问题。  

使用方法没project插件那么复杂,只要在项目的根目录下面放一个叫project.vim的文件就行了。该方法来源于这里：   http://easwy.com/blog/archives/automatically_update_ctags_tag_cscope_database/#comment-10782 ，project.vim不仅仅是项目标识，同时也是项目的配置文件。  

在vim里cd到项目目录中，或者直接打开项目中的文件，然后用“:MPLoad”载入project.vim及tags、cscope数据库（假如存在的话）。  

用“:MPBuildTags”可以建立tags或cscope数据库  

用“:MPUpdateTags”更新当前文件的tags或cscope数据库  

用“:MPSearchInProject 字符串”在项目中递归搜索。grep可用的话会调用grep，否则使用内部的vimgrep。  

假如安装了NerdTree，可以用“:MPNERDTREE”直接打开项目根目录  

在vimrc里写上“let g:MP_Write_AutoUpdate = 1”就会在每次保存文件时自动更新tags，想临时禁用自动更新的话就输入“:let g:MP_Update_Enable = 0”  

一些用于配置的全局变量：  
    
    " 项目文件名
    let g:MyProjectFileName = 'project.vim'
    " 是否启用ctags
    let g:MP_Ctags_Enable = 1
    " 是否启用cscope
    let g:MP_Cscope_Enable = 1
    " 定义ctags的路径
    let g:MP_Ctags_Path = 'ctags'
    " 定义cscope的路径
    let g:MP_Cscope_Path = 'cscope'
    "设置grep的路径
    " Tips: 如果是在windows下使用cygwin的grep的话，搜索结果中经常会出现警告，需要在系统中添加一个名叫CYGWIN，值为nodosfilewarning的环境变量
    let g:MP_Grep_Path = 'grep'
    " 定义ctags参数,比如c++项目可以在project.vim中定义"--c++-kinds=+px"
    let g:MP_Ctags_Opt = ''
    " 在文件写入时是否自动更新tags
    let g:MP_Write_AutoUpdate = 0
    " 是否自动载入项目文件
    let g:MP_Bufread_AutoLoad = 0
    " 是否允许更新tags(适合临时设置禁用或启用)
    let g:MP_Update_Enable = 1
    " 是否允许载入tags(适合临时设置禁用或启用)
    let g:MP_Load_Enable = 1
    " 需要建立tags的文件后缀名(可以针对不同项目在各自的project.vim文件中定义)
    let g:MP_Source_File_Ext_Name = 'c,h,cpp,vim,php,py'
    
更具体的使用方法就直接看代码吧，里面的注释还是蛮详细的。  

发一个我的配置  

    let g:MP_Bufread_AutoLoad = 1
    let g:MP_Source_File_Ext_Name = 'htm,js,c,h,cpp,vim,php,py,asp'
    map <f3> <esc>:MPSearchInProject <c-r>=expand("<cword>")<cr><cr>
    map <silent><f5> <esc>:MPLoad<cr>
    map <silent><f6> <esc>:MPUpdateTags<cr>
    
    if has("cscope")
        set cscopequickfix=s-,c-,d-,i-,t-,e-
        set cscopetagorder=0
        set cscopetag
        set nocscopeverbose
        nmap <C-@>s :cs find s <c-r>=expand("<cword>")<cr><cr>:copen<cr>
        nmap <C-@>g :cs find g <c-r>=expand("<cword>")<cr><cr>
        nmap <C-@>c :cs find c <c-r>=expand("<cword>")<cr><cr>:copen<cr>
        nmap <C-@>t :cs find t <c-r>=expand("<cword>")<cr><cr>:copen<cr>
        nmap <C-@>e :cs find e <c-r>=expand("<cword>")<cr><cr>:copen<cr>
        nmap <C-@>f :cs find f <c-r>=expand("<cfile>")<cr><cr>:copen<cr>
        nmap <C-@>i :cs find i ^<c-r>=expand("<cfile>")<cr>$<cr>:copen<cr>
        nmap <C-@>d :cs find d <c-r>=expand("<cword>")<cr><cr>:copen<cr>
    endif