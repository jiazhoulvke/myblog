+++
title = "时隔两年，myproject终于更新了"
categories = ["原创"]
tags = ["myproject","vim"]
date = "2014-02-08 00:00:00"
slug = "shigeliangnian，myprojectzhongyugengxinliao"
url = "/2014/02/08/e697b6e99a94e4b8a4e5b9b4efbc8cmyprojecte7bb88e4ba8ee69bb4e696b0e4ba86/"
draft = false
+++

[2012年6月我写了myproject这个插件](http://www.jiazhoulvke.com/170.html)，还只是个半成品，不过凑合着也能用，就这样一直用下去了。每次想完善一下的时候就想着先凑合着用，等有时间再改，就这样居然拖了近两年……这次终于下定决心，利用过年前的空闲时间完全重写了myproject。其实真的写起来一天就搞定了，剩下几天都是测试、修复bug。

## 更新内容

* 最开始的版本是纯vimscript的，后来因为在windows下更新tags时会弹出命令行窗口就加入了一部分python代码，现在为了兼容性还是改回了纯vimscript，不再依赖python。
* 增加 :MPCreate 命令，可以通过此命令创建项目。
* 增加 :MPProjectList 命令，可以浏览、删除、载入通过 :MPCreate 创建的项目。
* 保存、载入Session的命令从 :MPSaveSession、:MPLoadSession 改成了 :MPSessionSave、:MPSessionLoad。
* :MPCreate、:MPLoad、:MPSessionLoad、:MPSessionSave等命令都可以补全了。
* 去掉几个实用性不大的选项。
* 修改了部分变量名。

## 命令说明

### :MPCreate

* 直接输入 :MPCreate ，myproject会让你输入项目的路径及名称，然后会将该项目保存到项目列表中。当你用 :MPLoad 载入项目时就可以利用Tab自动补全项目路径了。
* 加入"template"参数(即:MPCreate template)，myproject会在项目中的project.vim文件中写入如下内容:

> "let g:MP_Ctags_Enable = 1  
> "let g:MP_Global_Enable = 1  
> "set cscopeprg=gtags-cscope  
> "let g:MP_Cscope_Enable = 1  
> "let g:MP_Session_AutoSave = 1  
> "let g:MP_Session_AutoLoad = 1  
> "let g:MP_Write_AutoUpdate = 1  
> "let g:MP_Source_File_Ext_Name = ""

你可以按自己的需求去掉某个选项的注释。

* 加入"question"参数(即:MPCreate question)，myproject会一一询问你是否需要开启某个选项，然后将结果保存到project.vim中。见下图:

[![MPCreate_question.png](http://www.jiazhoulvke.com/wp-content/uploads/2014/02/MPCreate_question.png)](http://www.jiazhoulvke.com/wp-content/uploads/2014/02/MPCreate_question.png)

### :MPProjectList

输入 :MPProjectList 会打开项目列表窗口，列出所有你创建的项目。

[![MPProjectList.png](http://www.jiazhoulvke.com/wp-content/uploads/2014/02/MPProjectList.png)](http://www.jiazhoulvke.com/wp-content/uploads/2014/02/MPProjectList.png)

移动光标到到你需要载入的项目上，按回车即可载入。按d则删除项目。

按小写的c会调用:MPCreate，按大写的C会调用:MPCreate question。

按q或者ESC会关闭项目列表窗口。

### :MPLoad

输入":MPLoad "后按Tab可以自动补全项目列表中的项目。

[![MPLoad.png](http://www.jiazhoulvke.com/wp-content/uploads/2014/02/MPLoad.png)](http://www.jiazhoulvke.com/wp-content/uploads/2014/02/MPLoad.png)

### :MPSessionSave

直接输入 :MPSessionSave 会将Session保存在项目根目录的default.session.vim文件中。

假如输入":MPSessionSave abc"则会保存到abc.session.vim。

### :MPSessionLoad

直接输入 :MPSessionLoad 会载入默认的session文件default.session.vim。

假如输入":MPSessionLoad abc"则会载入abc.session.vim。

输入":MPSessionLoad "后按Tab可以自动补全项目根目录中所有后缀为".session.vim"的文件名。

[![MPSessionLoad.png](http://www.jiazhoulvke.com/wp-content/uploads/2014/02/MPSessionLoad.png)](http://www.jiazhoulvke.com/wp-content/uploads/2014/02/MPSessionLoad.png)

## 变量说明

> g:MP_ProjectList 项目列表文件。默认值: globpath($HOME, '.MP_ProjectList.vim')
> 
> g:MP_ProjectFile 项目文件名。默认值: 'project.vim'
> 
> g:MP_Window_Height 项目列表高度。默认值: '10'
> 
> g:MP_Auto_Close 选择项目后是否自动关闭项目列表。默认值: 1
> 
> g:MP_Ctags_Enable 是否启用ctags。默认值: 0
> 
> g:MP_Ctags_Path 定义ctags的路径。默认值: 'ctags'
> 
> g:MP_Ctags_Opt 定义ctags参数。默认值: ''
> 
> g:MP_Global_Enable 是否启用GNU global。默认值: 0
> 
> g:MP_Global_Path 定义GNU Global的路径。默认值: 'global'
> 
> g:MP_Gtags_Path 定义gtags的路径。默认值: 'gtags'
> 
> g:MP_Cscope_Enable 是否启用cscope。默认值: 0
> 
> g:MP_Cscope_Path 定义cscope的路径。默认值: 'cscope'
> 
> g:MP_Source_File_Ext_Name 需要建立tags的文件后缀名,如:'c,h,cpp'。默认值: ''
> 
> g:MP_ConfigTitleBar_Enable 是否允许设置标题栏。默认值: 0
> 
> g:MP_TitleString 标题栏字符串。默认值: 
>     
>     %t\ %m%r\ [%{expand(\"%:~:.:h\")}]\ [ProjectPath=%{g:MP_Path}]\ -\ %{v:servername}
> 
> g:MP_Session_AutoSave 是否自动保存项目session。默认值: 0
> 
> g:MP_Session_AutoLoad 是否自动加载项目session。默认值: 0
> 
> g:MP_DefaultSessionName 项目默认session文件名。默认值: 'default'
> 
> g:MP_Session_Opt Session选项。默认值: "blank,buffers,curdir,folds,globals,options,resize,tabpages,winpos,winsize"
> 
> g:MP_Path 项目路径。载入项目时插件会自动修改该变量，请勿手动设置。
> 
> g:MP_Write_AutoUpdate 在文件写入时是否自动更新tags。默认值: 0
> 
> g:MP_Bufread_AutoLoad 读入文件时是否自动载入项目文件。默认值: 0