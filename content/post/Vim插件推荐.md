+++
title = "Vim插件推荐"
categories = ["原创"]
tags = ["vim"]
date = "2011-07-05 00:00:00"
slug = "Vimchajiantuijian"
url = "/2011/07/05/vime68f92e4bbb6e68ea8e88d90/"
draft = false
+++

1.pathogen([http://www.vim.org/scripts/script.php?script_id=2332](http://www.vim.org/scripts/script.php?script_id=2332))

pathogen是用来管理插件的插件。vim的插件是混在一起的，这在插件少的时候没什么问题，但当插件数量达到两位数时，问题就出来了——当我们下载试用某个插件，发现并不适合自己或者此插件和自己原来的插件有某些冲突时，你会发现很难清理掉刚刚安装的插件，因为有的插件有多达上百个文件，分布在不同的文件夹中。如果此插件是个vba包，那倒没什么问题，它可以像你在系统里安装的软件一样，通过一句命令清除掉,但问题是有些插件就是一个压缩包而已，并没有安装记录。这时pathogen就派上用场了，它会把每个插件放到各自的文件夹中，不需要用的时候直接删掉这个文件夹就行了，实在是很方便。

2.fencview([http://www.vim.org/scripts/script.php?script_id=1708](http://www.vim.org/scripts/script.php?script_id=1708))

这个插件的功能就是识别文件编码，对国人来说很有用。安装后可以在菜单项里找到识别编码的选项，不过用vim到一定程度的人，应该都不会还保留着菜单栏的吧？我的vimrc里加了一句:
    
    nmap <leader>fenc <esc>:FencAutoDetect<cr>

需要识别的时候通过快捷键就能识别了。还可以设置自动识别编码:

    let g:fencview_auto_patterns='*.txt,*.htm{l\=},*.php,*.c,*.py'

3.neocomplcache([http://www.vim.org/scripts/script.php?script_id=2620](http://www.vim.org/scripts/script.php?script_id=2620))
vim的补全插件里我最喜欢的一个。不像其他补全插件实时查找，而是在缓存中查找，用起来感觉很快。我的配置:
    
    let g:neocomplcache_enable_at_startup=1
    let g:neocomplcache_enable_smart_case=1
    let g:neocomplcache_enable_camel_case_completion=1
    let g:neocomplcache_enable_underbar_completion=1
    let g:neocomplcache_min_syntax_length=3
    let g:neocomplcache_manual_completion_start_length=3
    let g:neocomplcache_enable_ignore_case=1
    let g:neocomplcache_lock_buffer_name_pattern='\*ku\*'
    let g:neocomplcache_max_list=100
    let g:neocomplcache_enable_auto_select = 1
    imap <expr><c-y> neocomplcache#close_popup()
    imap <expr><c-e> neocomplcache#cancel_popup()

4.taglist([http://www.vim.org/scripts/script.php?script_id=273](http://www.vim.org/scripts/script.php?script_id=273))
类似于一些IDE，会在左边显示一个函数、变量列表(当然通过配置也可以显示在右边)，需要跳转到指定的函数时直接在函数名上面按回车即可。此插件需要ctags的支持。
我的配置:
    
        map <silent><f6> <esc>:TlistToggle<cr>

5.nerdtree([http://www.vim.org/scripts/script.php?script_id=1658](http://www.vim.org/scripts/script.php?script_id=1658))
vim里的文件管理器,以前我用的是winmanager，但这个nerdtree更好用。
我的配置:

    nmap <silent><f8> <esc>:NERDTreeToggle<cr>

6.tabbar([http://www.vim.org/scripts/script.php?script_id=1338](http://www.vim.org/scripts/script.php?script_id=1338))
类似于以前常用的minibufexpl，可以在顶部显示出已打开的buffer的列表，就像现在浏览器上的标签栏一样。tabbar比起minibufexpl更强大的功能是，它可以通过alt+数字直接在各个buffer中切换，还可以通过ctrl+tab轮换。

7.mark([http://www.vim.org/scripts/script.php?script_id=2666](http://www.vim.org/scripts/script.php?script_id=2666),旧版:http://www.vim.org/scripts/script.php?script_id=1238)
此插件的功能很简单，将光标移动到你需要高亮显示的关键字上面,比如test，按下&lt;leader&gt;m，则该文件中的所有test都会高亮显示。也许你会说，vim搜索的时候不是也可以高亮吗？是的，但是它只能高亮一个关键字，而mark可以同时高亮多个关键字，并且每个关键字都有不同的颜色(当你标记的关键字多的时候看起来非常漂亮)，这在阅读一些代码时非常好用。

8.project([http://www.vim.org/scripts/script.php?script_id=69](http://www.vim.org/scripts/script.php?script_id=69))
用来管理项目的插件。手头有一些比较大的项目需要管理时，这个插件就显得非常有用。

9.zencoding([http://www.vim.org/scripts/script.php?script_id=2981](http://www.vim.org/scripts/script.php?script_id=2981))
一个可以快速编写html代码的插件。比如输入 html:xt ,然后按 &lt;C-y&gt;, ，就会生成一大段的html代码，类似于snip,但在某些方面来说比snip更灵活更智能一点，具体不太好说，要用过才能体会。

10.vimpress([http://www.vim.org/scripts/script.php?script_id=3510](http://www.vim.org/scripts/script.php?script_id=3510),旧版:http://www.vim.org/scripts/script.php?script_id=1953)
直接在vim里发表、管理你的wordpress博客