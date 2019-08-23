# Micropython快速开始 {docsify-ignore-all}

## 连接你的喵比特(前提须知)

成功将喵比特通过USB与电脑连接后，喵比特的屏幕应显示如下界面（我们就称之`bootloader界面`）  

![](https://s2.ax1x.com/2019/05/27/VZleR1.jpg)  

!> 如果不是这个界面，则检查一下喵比特头上的电源开关是否打开(置向左边),或者USB连接是否稳定。

## 进入micropython模式

1. 喵比特可选两种编程模式，一种是Arcade游戏编程模式，一种是micropython纯代码编程。程序文件下载入口是bootloader界面，使用者暂时只需要了解这个界面下只支持拖入.uf2的格式文件执行。
    - Arcade的程序文件就是.uf2
    - 此时micropython模式就像是附带品一样，同样通过一个.uf2的程序引导模式开启。

2. 下载这个引导程序文件 http://cdn.kittenbot.cn/meowbit/meowpy.uf2 <sup style="color:red" class="animated infinite flash">2019.8.1 NEW</sup>
3. 将该文件拖入ARCADE-F4盘符下(如果你在bootloader界面，电脑就会对应出现这个名称盘符)
<p style = "text-align:center" >▼</p>
  
![](https://s2.ax1x.com/2019/05/27/VZ83oF.png ':no-zoom')  

- 待进度条走完后，注意喵比特的屏幕，不出意外会黑屏，随即可以看到出现`PYBFLASH`字样的盘符。此时你已经成功进入micropython模式界面  

!>如果它的名字是*可移动磁盘*，则需要按1下右侧边上面第一颗按键（RESET键），返回到bootloader界面后，按住A键不放，同时再次按1下RESET键。此时可见盘符为PYBFLASH字样无误  

?>刷入了micropython模式固件后，在bootloader界面下，通过同时按住A和RESET的作用为初始化刷新FlASH

## 文件介绍
    
打开这个新的磁盘可以看到里面有如下文件
![](https://s2.ax1x.com/2019/08/23/mBRKht.png ':no-zoom')    

- boot.py 是启动文件，一上电micropython会最优先执行这个文件，一般包括所有运行环境和库文件的初始化，它指定了当你开机后首先运行的是名字为main的.py程序
- main.py 是用户的主程序，大家平时学习开发主要是编辑这个文件
- pybcdc.inf 是串口驱动安装文件


## 编程软件
  
高手会直接选用编辑器来编程，每次只需要保存一下main.py就等于烧录了新的程序，如果程序没有任何错误，那么刷新(即间断按下2次复位切到bootloader界面再切回来就可以看到你要的程序正在执行)，如果你的程序存在错误，那么喵比特右上角的两颗灯会交替闪烁一会儿。如果你是在找不到错在哪，为了方便起见建议还是使用Mu editor 

![](https://s2.ax1x.com/2019/05/27/VZtntU.png ':no-zoom')  

新人当然是推荐使用Mu edtior作为编程软件。优势在于：  
- 支持一键REPL(在线调试)
- 支持一键查语法错误bug等  

[下载地址](http://cdn.kittenbot.cn/mu/Mu_1.1.0a1.exe)

![](https://s2.ax1x.com/2019/05/27/VZtlc9.png ':no-zoom')  

!> 下载过程请关闭360等杀毒软件，避免误删，下载完成后软件图标会出现在开始菜单中

## 安装串口驱动(这一点win10或mac用户可以忽略)
  

!>为了能让喵比特在Mu editor中通过REPL实现在线交互，我们需要像Microbit在kittenblock中那样有一个串口驱动，而win10和mac则会自动安装  

<!-- 首先需要下载这个文件 http://cdn.kittenbot.cn/meowbit/pybcdc.inf   -->

1. 刚切换至Micropython模式时可以看到电脑正试图安装驱动，但串口驱动的安装会失败，在设备管理器中可以看到。  

![](https://s2.ax1x.com/2019/01/29/kQNF74.png)  

!> 如果你不太清楚设备管理器怎么查看，请跟随如下步骤
![](https://s2.ax1x.com/2019/05/27/VZNBPU.png)  
![](https://s2.ax1x.com/2019/05/27/VZNgq1.png)

2. 在PYBFLASH的盘符内可见.ini格式文件，我们使用它令安装串口驱动能顺利安装

![](https://s2.ax1x.com/2019/05/27/VZU2lQ.png ':no-zoom')   

3. 右键点击1.中打感叹号的Pyboard设备，并按照顺序点击 更新驱动程序软件->浏览计算机以查找驱动程序软件->浏览->选择可移动磁盘->下一步即可

![](image/mode_4.png ':no-zoom')  
  
4. 如果一切顺利，可以看到驱动安装成功后在设备管理器下多出来一个新的串口设备  
  
![](https://s2.ax1x.com/2019/01/29/kQURJA.png ':no-zoom')  
  
!>如果出现安装错误等安装失败的问题，请查阅  [解决串口驱动安装失败](micropython/meowbit驱动安装失败的问题解决)

## 通过Mu editor来编辑第一个mian.py程序

确保此时处于Micropython编程界面下

**打开Mu editor**
当你正确连接好喵比特，软件将自动检测并切换到Meowbit编程模式，如果出现如下提示选择OK既可

![](https://s2.ax1x.com/2019/05/27/VZwnSS.png ':no-zoom')   

**编辑主程序**
此时你可以看到界面如下  
![](https://s2.ax1x.com/2019/08/23/mBfITH.png)  

这是由于Mu检测到了你已经连上电脑，会自动打开你文件中的main.py（如果没有，你可以点选导功能栏中的加载并找到喵比特盘符选择里面的main.py文件）。上图的颜色可能和你的原始Mu不一样，你可以通过主题按钮来切换

**初识程序结构**
初步认识下python的语法    
我们先将如下程序段复制到第二行
```python
import pyb
import framebuf

fbuf = bytearray(160*128)
fb = framebuf.FrameBuffer(fbuf, 160, 128, framebuf.PL8)
tft = pyb.SCREEN()
fb.fill(8)
fb.text('Hello Micropython!', 10, 50, 2)
tft.show(fb, 1)
```

![](https://s2.ax1x.com/2019/05/27/VZwOXQ.png)

<p style = "display:inline">①.</p> <p style = "color:#999;display:inline;"># main.py -- put your code here!</p>  

在第一行你可以看到# 开头的一行异色字体，它代表着注释，这一行将不会被系统识别，也就不会做任何事情，只用于方便人为阅读。  

!> 如果不是单独起一行，而是直接跟在程序代码后面则需要确保相距2个字符空位以上，一般使用Tab键隔开即可

②.
<p style = "color:#3A3;line-height:2px;">import pyb</p>  
<p style = "color:#3A3;line-height:2px;">import framebuf</p>   

import用于导入模块，模块内包含的是可调用的功能函数和方法。

!> pyb这个模块包含了控制喵比特功能的所有功能函数和方法，在蓝色背景红色字符的默认程序中，使用pyb模块来驱动显示屏，framebuf模块则提供一般的帧缓冲区，可用于创建位图图像，然后将其发送到显示屏(简单来说就是有了这个模块我们就可以给屏幕显示提供数据了)

③.这个部分就是程序主体，你想要实现的功能都在这部分编些。
好比我们此时看到的喵比特屏幕所显示的蓝色背景和红色字符。

**改写你的第一个程序**

将界面中所有代码删掉，开始写我们第一个python程序吧。  

1. 首先我们需要加载pyb模块

import pyb

2. 第二行我们写点亮喵比特右上角第一个绿灯，需要调取pyb模块中的LED类，先创建一个LED(1)，然后将它置on  

pyb.LED(1).on()  

3. 整合起来代码如下：  

```python
import pyb	# 该模块包含所有函数和类来控制喵比特的功能
pyb.LED(1).on()  
```

**保存程序**
过程中可以看到喵比特右上角的绿灯常亮一阵，然后熄灭即程序下载成功
![](https://s2.ax1x.com/2019/05/27/VZ2i3n.png)

**运行新程序**
喵比特每次引导进入micropython模式都只会执行上一次最新的main.py，但如果我们更改了程序，就需要间通过reset按键来重启引导进入新程序：间断按2下reset按键(第一下切到bootloader界面，第二下切回micropython模式等待程序运行)

!> 如果在再次进入micropython模式的时候出现了红绿灯双闪的情况，则需要检查程序在哪一部分出错。  

## 充分运用Mu的REPL  

**在线调试功能**

当你写好了一个比较长的程序，程序哪怕是错了一个符号也会存在无法运行的情况，若你没有十足的信心，此时我们会使用REPL对程序分段进行调试。  

!> 此处默认你已经完成了上述的所有流程包括串行驱动安装，然后确保你的喵比特与USB连接正常而且整处于micropython模式下。  

1. 点击功能栏里的`REPL`

![](https://s2.ax1x.com/2019/05/27/VZhHyR.png)  

提示栏出现在界面下方并且每一行开头都有>>>的符号，初次建立连接后可以多按几次回车键测试它是否正常工作，如果正常你能看到在后面会多出几行>>>，之后将需要调试的程序打在这后面 

!> 每一个>>>后只能跟一行代码，每键入一行代码需按下回车执行，如果出错则会报错。如若想要跟多行代码，可以通过同时按下Ctrl+Shift+E。按下后会出现如下===的提示符(如果没有出现可能是输入法导致，切一下即可)
![](https://s2.ax1x.com/2019/05/27/VZ4K6s.png)  
之后将你需要的代码段确认无误后全部选中并复制，在===后右键选择`Paste`，以点灯的代码为例，就可以看到如下软件会帮你自动换行，之后根据提示按下Ctrl+D执行
![](https://s2.ax1x.com/2019/05/27/VZ4YhF.png)  

2. 尝试输入并熟悉各种功能实现代码,且每输入一行都按下回车查看返回结果 

 <i>>>></i> a = 1  
 <i>>>></i> a  
 <i>>>></i> b = 3  
 <i>>>></i> b  
 <i>>>></i> a = 1    
 <i>>>></i> print('a + b = '+ str(a + b))  
 <i>>>></i> pyb.LED(2).on()  
 <i>>>></i> pyb.LED(2).off()    

当你输入最后两行可以看到喵比特右上角的红灯亮又灭了  

!> 通过REPL调试的可以直接使用的模块只可以是pyb模块和main.py文件本已经import过的模块。如果需要使用其他模块功能要记得先import。每次保存main.py后，需要关闭现有的REPL再重新打开


## REPL使用小技巧 

**REPL记录输入历史**  
通过方向键↑，可以调出上一次键入的代码，也可以通过↓回撤  

**Tab键**  
补全代码或查看模块中所有方法
- 补全代码：当你已经导入需要的模块，在模块中有些方法名记不太全但记得开头可以使用tab，如pyb.L按下Tab，它会出来唯一代码行pyb.LED，我们只需要键入后面的参数即可。
- 查看模块所有方法，当你键入pyb.按下Tab，会出现pyb模块所包含的所有函数方法。![](https://s2.ax1x.com/2019/05/27/VZo9l4.png) 




