---
layout:     post
title:      SearchKey-自建全网寻找关键字工具
subtitle:   批量大法好
date:       2018-10-19
author:     蓝胖
header-img: img/post-bg-2018-10-19.jpg
catalog: true
tags:
    - Python
    - Tools


---

>“你的心灵是疯狂与天才的奇妙组合。我刚把天才那部分拿走了”



 > 发现一个可以批量操作的思路，谷歌找也找不到多少结果，fofa可以搜到不少，看是没会员，哭。就自己动手做一个工具吧。代码能力一般，能用就好~ 

# 简介

`SearchKey` 是一款可以验证全网IP是否存在自己需要的关键字的工具，配合`masscan`简直完美！

# 特色

 1. 自定义自己需要的关键字
 2. 自定义线程数量
 3. 自定义端口

# 使用方法

```
C:\>python3 SearchKey.py -h
usage: Check_Url [-h] [-k KEY] [-i INPUT] [-o OUTPUT] [-t NUM] [-p PORT]

optional arguments:
  -h, --help            show this help message and exit
  -k KEY, --key KEY     Keyword
  -i INPUT, --input INPUT
                        file for scanning
  -o OUTPUT, --output OUTPUT
                        file for scanning results
  -t NUM, --thread NUM  Number of threads for program
  -p PORT, --port PORT  Port of scanning
```


![iw4V4f.png](https://s1.ax1x.com/2018/10/19/iw4V4f.png)

# 说明
```
Pyhon3 
默认读取文件是input.xml,输出文件是output.txt
默认80端口、20线程
```

# 地址
[GitHub](https://github.com/lanpan999/SearchKey)
