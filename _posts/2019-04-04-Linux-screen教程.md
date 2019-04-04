---
layout:     post
title:      Linux-screen教程
subtitle:   创建多窗口
date:       2019-04-04
author:     蓝胖
header-img: img/post-bg-2019-04-04.jpg
catalog: true
tags:
    - Linux
    
---

>“要么学！要么不学！学和不学之间没有中间值 不学就放弃,学就要去认真的学！”


   这个是去年葛老师教我的，最近又用到了，想想还是记录下

 
## screen命令是什么
> Screen是一个可以在多个进程之间多路复用一个物理终端的全屏窗口管理器。Screen中有会话的概念，用户可以在一个screen会话中创建多个screen窗口，在每一个screen窗口中就像操作一个真实的telnet/SSH连接窗口那样。

## 如何安装screen

CentOS系统可以执行：*yum install screen*

Debian/Ubuntu系统执行：*apt-get install screen*

## 使用方法
### 创建screen会话
执行：*screen -S temp* ，screen就会创建一个名字为temp的会话

### 暂时离开会话
当需要临时离开时（会话中的程序不会关闭，仍在运行）可以用快捷键Ctrl+a d(即按住Ctrl，依次再按a,d)


### 恢复screen会话
当回来时可以再执行执行：*screen -r temp* 即可恢复到离开前创建的temp会话的工作界面。如果忘记了，或者当时没有指定会话名，可以执行：screen -ls screen会列出当前存在的会话列表

### 关闭screen的会话
执行：exit ，会提示：[screen is terminating]，表示已经成功退出screen会话


## 常用快捷键
Ctrl+a c ：在当前screen会话中创建窗口
Ctrl+a w ：窗口列表
Ctrl+a n ：下一个窗口
Ctrl+a p ：上一个窗口
Ctrl+a 0-9 