---
layout:     post
title:      Python版的Burp-Sqlmap插件
subtitle:   Burp插件
date:       2019-04-05
author:     蓝胖
header-img: img/post-bg-2019-04-05.jpg
catalog: true
tags:
    - Burp
    - Sqlmap
    
  
---

>“先去尝试你最想做的东西，不用考虑太多。竭尽全力去试。如果真的不可为之的话，再回到你只能去做的东西，这时候也能踏踏实实做出成绩来，不再疑惑。—— Drew G. Faust”

#### 为什么做这个
在使用java版的sqlmap插件，总是无法正常运行，自己太菜排查了好久，还没办法解决。于是就尝试着自己做个Python版的插件，而且以后还可以做其他形式的。比如fuzz、SSRF等等。 

# 效果
* 普通get注入
* post+leve2注入
* post+leve5注入
* 全自动下一步、发现注入点有提示音
[![ATnTUK.png](https://s2.ax1x.com/2019/04/10/ATnTUK.png)](https://imgchr.com/i/ATnTUK)
[![ATn5Hx.md.png](https://s2.ax1x.com/2019/04/10/ATn5Hx.md.png)](https://imgchr.com/i/ATn5Hx)
[![ATn4D1.md.png](https://s2.ax1x.com/2019/04/10/ATn4D1.md.png)](https://imgchr.com/i/ATn4D1)

# 安装
burp需要jython的支持。下载安装jython到 **C:\jython2.7.0** [jython](https://www.jython.org/downloads.html)

将py-sqlmap.py放到sqlmap文件目录。 比如我的目录是：**C:\jython2.7.0\plung\sqlmap**
然后去burp中添加 py-sqlmap.py
[![ATnoE6.md.png](https://s2.ax1x.com/2019/04/10/ATnoE6.md.png)](https://imgchr.com/i/ATnoE6)
[![ATnhuR.png](https://s2.ax1x.com/2019/04/10/ATnhuR.png)](https://imgchr.com/i/ATnhuR)


# 需要注意的地方
因为我用的是Python双环境，如果提示Python2 不存在，把代码中83、99、115行的Python2 改成Python就行