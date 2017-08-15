---
layout: post
title: "在Ubuntu中显示中国味的汉字"
date: 2017-08-15 10:49:26 +08:00
description: 在Ubuntu中用“中国味”而不是“日本味”来显示汉字
share: true
tags: linux
---

在使用的 ubuntu 16.04 默认使用的“宋体”字体，显示汉字像日本字，不舒服。 
例如这个词：“准确”，在 console 中显示的汉字明显带着日本味。 
 
![cnfont-fail]({{site.baseurl | prepend:site.url}}/images/cnfont-fail.png){:width=220px}
 
经尝试，使用 Noto Sans CJK SC 显示的汉字是正常的，一定是字体相关配置有问题。 
 
改善办法: 
 
修改 /etc/fonts/conf.avail/69-language-selector-zh-cn.conf 配置文件， 
把其中的所有关于 lang 的 test 项全部注释掉: 
 
    <test name="lang"> 
        <string>zh-cn</string> 
    </test> 

 
改为 
 
    <!-- 
    <test name="lang"> 
        <string>zh-cn</string> 
    </test> 
    --> 
 
然后关闭所有桌面程序，并重启桌面。 
 
    $ sudo service lighdm restart 
 
然后，在 console 中就能得到纯正的中国味汉字了: 
 
![cnfont-ok]({{site.baseurl | prepend:site.url}}/images/cnfont-ok.png){:width=220px}
 
