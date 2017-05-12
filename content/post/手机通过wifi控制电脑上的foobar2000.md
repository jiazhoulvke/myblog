+++
title = "手机通过wifi控制电脑上的foobar2000"
categories = ["原创"]
tags = ["Go"]
date = "2012-04-29 00:00:00"
slug = "shoujitongguowifikongzhidiannaoshangdifoobar2000"
url = "/2012/04/29/e6898be69cbae9809ae8bf87wifie68ea7e588b6e794b5e88491e4b88ae79a84foobar2000/"
draft = false
+++

必须先感叹一句，GO语言太强了，自带的库很丰富，语法够简洁，即使没接触过GO，稍微学习一下就能用几十行代码做出个简单的web服务器。

由于foobar2000可以通过命令行进行操作，比如:

    foobar2000.exe /command:Next

就是切换到下一曲。利用这个特性，就能很轻易的实现远程操控foobar2000。

下面是GO语言的代码,文件名为foobar2k_web.go:

    package main
    
    import (
        "os/exec"
        "fmt"
        "io"
        "net/http"
        "os"
    )
    
    var service_port   = ":9527"
    var service_path  = "/foobar2k"
    var foobar2k_path = "d:\\bin\\foobar2000\\foobar2000.exe"
    var fbcmd_map     = map[string]string{"prev":"Previous","next":"Next","vdown":"Down","vup":"Up","playpause":"Play or pause"}
    
    func FB2KServer(w http.ResponseWriter, req  *http.Request) {
        io.WriteString(w, "")
        io.WriteString(w, "")
        io.WriteString(w, "")
    	io.WriteString(w, "<style type="\&quot;text/css\&quot;">div.bt {width:100px;height:100px;float:left;text-align:center;line-height:100px;background-color:green;}div.bt a{font-size:72px;color:white;font-weight:bold;text-decoration:none;}</style>")
        io.WriteString(w, "")
        io.WriteString(w, "")
    	io.WriteString(w, "<div style="\&quot;width:500px;height:100px;margin:100px" auto;\"="">")
        io.WriteString(w, "<div class="\&quot;bt\&quot;"><a target="\&quot;_self\&quot;" href="\&quot;&quot;+service_path+&quot;?fbcmd=prev\&quot;">《</a></div>")
        io.WriteString(w, "<div class="\&quot;bt\&quot;"><a target="\&quot;_self\&quot;" href="\&quot;&quot;+service_path+&quot;?fbcmd=next\&quot;">》</a></div>")
        io.WriteString(w, "<div class="\&quot;bt\&quot;"><a target="\&quot;_self\&quot;" href="\&quot;&quot;+service_path+&quot;?fbcmd=playpause\&quot;">||</a></div>")
        io.WriteString(w, "<div class="\&quot;bt\&quot;"><a target="\&quot;_self\&quot;" href="\&quot;&quot;+service_path+&quot;?fbcmd=vdown\&quot;">◣</a></div>")
        io.WriteString(w, "<div class="\&quot;bt\&quot;"><a target="\&quot;_self\&quot;" href="\&quot;&quot;+service_path+&quot;?fbcmd=vup\&quot;">◢</a></div>")
        io.WriteString(w, "</div>")
        io.WriteString(w, "")
        io.WriteString(w, "")
        var fbcmd = req.FormValue("fbcmd")
        cmd := exec.Command(foobar2k_path,"/command:"+fbcmd_map[fbcmd])
        cmd.Start()
    }
    
    func main() {
        http.HandleFunc(service_path,FB2KServer)
        fmt.Printf("started!");
        err := http.ListenAndServe(service_port ,nil)
        if err != nil {
            fmt.Printf("ERR:=%s\n",err)
            os.Exit(-1)
        }
    }

其中service_port定义的是端口号，service_path定义的是服务的路径，foobar2k_path定义的是foobar2000在电脑上的绝对路径,fbcmd_map定义的是foobar2000支持的操作命令，这里只定义了下一曲、上一曲、播放/暂停等常用命令。

用go编译后生成foobar2k_web.exe,双击运行后会弹出个控制台窗口，显示”started!”。

<img style="opacity: 1;" lazyloadpass="1" title="foobar2k_web.JPG" src="http://www.jiazhoulvke.com/wp-content/uploads/2012/04/foobar2k_web.jpg" file="http://www.jiazhoulvke.com/wp-content/uploads/2012/04/foobar2k_web.jpg" class="aligncenter lh_lazyimg"><noscript><img title="foobar2k_web.JPG" src="http://www.jiazhoulvke.com/wp-content/uploads/2012/04/foobar2k_web.jpg" class="aligncenter" /></noscript>

然后用手机连接wifi，访问 http://电脑端的ip:端口号/路径 ,比如我的电脑端的ip地址是192.168.1.3,定义的端口号是9527,定义的路径是/foobar2k，那么就可以访问 http://192.168.1.3:9527/foobar2k ，不出意外的话在手机上就能看到如下界面：

<img style="opacity: 1;" lazyloadpass="1" title="foobar2k_web_phone.png" src="http://www.jiazhoulvke.com/wp-content/uploads/2012/04/foobar2k_web_phone.png" file="http://www.jiazhoulvke.com/wp-content/uploads/2012/04/foobar2k_web_phone.png" class="aligncenter lh_lazyimg"><noscript><img title="foobar2k_web_phone.png" src="http://www.jiazhoulvke.com/wp-content/uploads/2012/04/foobar2k_web_phone.png" class="aligncenter" /></noscript>

点击手机上的按钮，foobar2000就会做出相应动作，假如foobar2000还没有启动的话，则会自动启动。

目前的程序功能还很简陋，要好用点还得再完善一下，比如定义的端口号、foobar2000路径都放到配置文件里，操作界面美化等。