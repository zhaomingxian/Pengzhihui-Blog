title: 蓝牙调试APP-可控
date: 2016-09-20 20:32:45
tags:
- 项目
- Android
------

> - 其实我很早之前就做过一个蓝牙的调试APP [蛋黄2.0](http://www.pengzhihui.xyz/2015/12/09/nano/)，那个版本只是配合小机器人进行一些无线控制。当时功能做的比较多，常用的调试模块都加上去了，但是很多软件细节一直没有完善，也由于没有时间写Arduino配套的库，所以就没有发布。最近也看到论坛很多小车啊机器人啊的项目，似乎有必要为大家提供一个完善的遥控和无线调试解决方案，所以又翻出这个工程，小通了个宵填上了这个遥远的坑。。。
> - APP取名叫【可控】，基本功能都已经完成了，已经发布在腾讯应用宝上，需要的可以自行下载体验，下面会详细介绍一下功能和使用方法。

![pic1](http://i2.tiimg.com/1949/f64c2a128727381e.gif)



## APP功能

APP是通过蓝牙连接蓝牙模块然后和硬件交互的，点击右上角的图标连接就行（当然模块需要事先在手机设置里配对），依次介绍一下各个标签的功能：

* **摇杆功能**：连接硬件后可以在程序里通过库函数读取到摇杆的数值，用于遥控小车什么的最方便啦，比如我之前的 [Qbot](http://www.pengzhihui.xyz/2015/11/05/qbot/) 就是用这个遥控的
* **重力感应功能**：跟摇杆一样，不过这里变成摇晃手机进行控制了，依然是可以在Arduino程序里读出数据
* **曲线功能**：提供3个通道数据的曲线绘制功能，曲线的数据可以在Arduino库函数里进行调用发送，方便用于调节参数之类的
* **串口助手功能**：前面几个模式都是可以调用库函数进行方便的交互的，但是如果只想按自己的指令来操作，或者只是想有个串口显示的窗口，就可以用到这个模块，既可以发送数据也可以接收，是完全透传的。


<!--more-->


## Arduino库函数的使用：

库函数的下载地址在文末，使用方法其实和之前的[迹](http://www.pengzhihui.xyz/2016/05/05/trace/)和[颜艺Boy](http://www.pengzhihui.xyz/2017/02/22/faceapp/)基本雷同，可以参考这两篇文章。不一样的是，由于前两者都只需要接收手机数据，所以可以使用软件串口来连接模块，这样的话可以自定义IO端口而且不影响程序的串口下载；但是由于软件串口在同时收发的时候会有丢包的BUG，所以在本APP中只能使用硬件串口连接（另一个原因是像曲线绘制功能需要较高的通信速率，所以硬件串口会可靠很多），这里非常建议使用带2个以上串口的板子如Mega，pro micro等，省去下载的时候拔插模块的麻烦。



## 结尾

APP后面还会继续完善，下一版本可能会加入自定义按键的功能，大家有什么使用问题和好的功能建议也可以在文章下留言~

[Arduino库下载](https://github.com/david-pzh/CtrlAPP-Arduino)