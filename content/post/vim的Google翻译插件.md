+++
title = "vim的Google翻译插件"
categories = ["原创"]
tags = ["google","python","translate","vim"]
date = "2012-04-14 00:00:00"
slug = "vimdiGooglefanyichajian"
url = "/2012/04/14/vime79a84googlee7bfbbe8af91e68f92e4bbb6/"
draft = false
+++

由于经常需要在vim里看一些英文帮助文档，又没有长年累月的运行一个翻译软件的习惯，所以还是写了个插件来搞定,用了python，所以windows下得确保安装了python。

![](/static/wp-content/uploads/2012/04/i1.png)

使用方法有几种：

1.将光标移动到需要翻译的英文单词上，按&lt;leader&gt;e2c(把中文翻译成英文就是&lt;leader&gt;c2e，下面就不多说了)。

![](/static/wp-content/uploads/2012/04/i2.png)

2.选中需要翻译的英文，按&lt;leader&gt;e2c。

3.输入
    
    :E2C 想要翻译的英文

优点：因为是调用Google进行翻译，所以Google能翻译多少种语言，插件就能翻译多少种语言，不过默认只map了英译中和中译英的快捷键，其他的得自己定义了。  

缺点：连不了网就死翘翘了。

快捷键定义方法举例:
    
    nmap <silent> <leader>e2c :echo Google_Translate('en','zh-CN',expand('<cword>'))<cr>

en是原文的语言，zh-CN是要翻译的语言。

下载地址:[http://code.google.com/p/jiazhoulvke/downloads/detail?name=googletranslate.vim](http://code.google.com/p/jiazhoulvke/downloads/detail?name=googletranslate.vim)

代码:

    " googletranslate.vim: 利用Google翻译在vim中进行翻译
    " Author:       jiazhoulvke
    " Blog:         http://jiazhoulvke.com
    " Date:         2012-4-10
    " Version:      1.0
    "-------------------------------------------------
    " Google_Translate: 谷歌翻译
    function! Google_Translate(lan1,lan2,word)
    python << EOM
    #coding=utf-8
    import vim,urllib,urllib2
    word = vim.eval("a:word")
    word=word.replace('\n','')
    rword = urllib.urlencode({'text':word})
    lan1 = vim.eval("a:lan1")
    lan2 = vim.eval("a:lan2")
    headers = {
        'User-Agent':'Mozilla/5.0 (Windows NT 6.1) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.15 Safari/536.5'
    }
    url = 'http://translate.google.com/translate_a/t?client=firefox-a&langpair;='+lan1+'%7c'+lan2+'&ie;=UTF-8&oe;=UTF-8&'+rword
    req = urllib2.Request(
        url = url,
        headers = headers
    )
    resultstr=''
    gtresult = urllib2.urlopen(req)
    if gtresult.getcode()==200:
        gtresultstr=gtresult.read()
        po=eval(gtresultstr)
        resultstr=''
        for poi in po['sentences']:
            resultstr+=poi['trans']
        if po.has_key('dict'):
            if len(po['dict'])>0:
                if po['dict'][0].has_key('terms'):
                    tr=','.join(po['dict'][0]['terms'])
                    resultstr+='\n'+word+':'+tr
    vim.command('let resultstr = "%s"' % resultstr)
    EOM
    return resultstr
    endfunction
    
    "-------------------------------------------------
    " Google_Translate_Selected_String: 翻译选中文本
    function! Google_Translate_Selected_String(lan1,lan2)
        normal `<
        normal v
        normal `>
        silent normal "ty
        return Google_Translate(a:lan1,a:lan2,@t)
    endfunction
    
    "-------------------------------------------------
    " Key_and_command_bind: 按键及命令绑定
    if !hasmapto('<leader>e2c','n')
        nmap <silent> <leader>e2c :echo Google_Translate('en','zh-CN',expand('<cword>'))<cr>
    endif
    if !hasmapto('<leader>c2e','n')
        nmap <silent> <leader>c2e :echo Google_Translate('zh-CN','en',expand('<cword>'))<cr>
    endif
    if !hasmapto('<leader>e2c','v')
        vmap <silent> <leader>e2c <esc>:echo Google_Translate_Selected_String('en','zh-CN')<cr>
    endif
    if !hasmapto('<leader>c2e','v')
        vmap <silent> <leader>c2e <esc>:echo Google_Translate_Selected_String('zh-CN','en')<cr>
    endif
    if !exists(":E2C")
        command! -nargs=+ E2C :echo Google_Translate("en","zh-CN",<q-args>)
    endif
    if !exists(":C2E")
        command! -nargs=+ C2E :echo Google_Translate("zh-CN","en",<q-args>)
    endif
    "-------------------------------------------------
    " Modelines: 
    " vim: ts=4 nowrap fdm=marker foldcolumn=1 ft=vim
