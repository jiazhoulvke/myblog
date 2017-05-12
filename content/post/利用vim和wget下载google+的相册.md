+++
title = "利用vim和wget下载google+的相册"
categories = ["原创"]
tags = ["vim","wget"]
date = "2012-11-28 00:00:00"
slug = "liyongvimhewgetxiazaigoogle+dixiangce"
url = "/2012/11/28/e588a9e794a8vime5928cwgete4b88be8bdbdgooglee79a84e79bb8e5868c/"
draft = false
+++

先找到相册地址，比如 https://plus.google.com/photos/113638836970166422741/albums/5812010190409709377 ，里面很多妹子，很合我的胃口。

右键查看源代码，复制到vim中（当然你也可以直接用wget下载网页）,然后执行
    
    :%s/"/\r/g
    :sort u

按 

    /^https.*jpg$

找到第一个图片链接,在它上面一行按dgg，再按N，反向查找最后一个图片链接，在它下面一行按dG，即可得到所有图片的地址。

由于留下的地址列表里包含两种缩略图，所以要删除缩略图，留下所有原图:
    
    :g/w800-h800\//d
    :g/s300-c\//d

将最后的结果保存：
    
    :w c:\mm.list

现在利用万能的wget批量下载。因为gfw的原因需要一个代理，我用的是goagent，在goagent已经运行的前提下输入:
    
    wget -i c:\mm.list -e http_proxy=127.0.0.1:8087 --no-check-certificate

之后慢慢等它下载好就行了。一个vim的简单应用。