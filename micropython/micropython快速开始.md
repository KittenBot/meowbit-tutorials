# Micropython快速开始 {docsify-ignore-all}

## 进入micropython模式

V2版本开始的喵比特在makecode和micropython编程模式中的切换变得十分方便。

- 首先下载必要文件 http://cdn.kittenbot.cn/meowbit/meowpy.uf2 
- 将该文件拖入MEOWBIT盘符下,如果没有看到盘符，可能你是从Makecode编程切过来使用Micropython的，任然在Makecode程序界面，此时按下复位键切至主界面。

![](image/mode_1.png ':no-zoom')
- 初次使用可以看到电脑中出现了一个`可移动磁盘`，屏幕中间显示字符`Hello Micropython`就能够顺利使用Micropython编程啦

## 重要文件介绍  
    
成功进入Micropython模式后电脑出现的盘符内会有几个基础文件  

![](image/mode_2.png ':no-zoom')    

- boot.py 是启动文件，一上电micropython会最优先执行这个文件，一般包括所有运行环境和库文件的初始化。
- main.py 是用户的主程序，大家平时学习开发主要是编辑这个文件，喵bit准备就绪后会自动执行这个文件的代码。
- unicode12.bin 是一个字库，里面包含了世界上几乎所有的语言。

## 开始编程  
  
高手当然可以选择直接使用编辑器打开main.py文件进行编程，每次只需要保存一下main.py就等于烧录了新的程序，如果程序没有任何错误，那么间断按下2次复位后刷新程序就可以看到你要的程序正在执行  

![](image/editor.png ':no-zoom')  

但是对于新人我们依然推荐使用编程软件，这里推荐MU editor [下载地址](http://cdn.kittenbot.cn/mu/Mu_1.0.1.exe) 

![](image/editor2.png ':no-zoom')  

## 安装串口驱动
  
这一步win10或mac用户可以忽略

首先需要下载这个文件 http://cdn.kittenbot.cn/meowbit/pybcdc.inf

!>为了能让喵比特在Mu editor中通过REPL实现在线交互，我们需要像Microbit在kittenblock中那样有一个串口驱动,win10和Mac多半都能自动成功安装无需看下述步骤

1. 刚切换至Micropython模式时可以看到电脑正试图安装驱动，但串口驱动的安装会失败，在设备管理器中可以看到。  

![](https://s2.ax1x.com/2019/01/29/kQNF74.png)  

2. 我们将下载好的.inf文件拖入到喵比特的可移动磁盘下 

![](image/mode_3.png ':no-zoom')   

3. 右键点击这个设备，并按照顺序点击 更新驱动程序软件->浏览计算机以查找驱动程序软件->浏览->选择可移动磁盘->下一步即可

![](image/mode_4.png ':no-zoom')  
  
4. 如果一切顺利，可以看到驱动安装成功后在设备管理器下多出来一个新的串口设备  
  
![](https://s2.ax1x.com/2019/01/29/kQURJA.png ':no-zoom')  
  
!>如果出现安装错误等安装失败的问题，请查阅  [解决串口驱动安装失败](micropython/meowbit驱动安装失败的问题解决)

## 通过Mu editor连接上喵比特


1. 确保此时处于Micropython编程界面下，也就是可以看到`可移动磁盘`这个盘符。接着我们打开Mu editor 

![](image/mode_5.png ':no-zoom') 

2. 当检测到喵比特，软件将自动提示切换到Meowbit，选择确定既可

![](image/mode_6.png ':no-zoom')   

若没有提示，则手动在模式下选择，也可能是串口驱动未安装成功，网上查看具体步骤 

![](https://s2.ax1x.com/2019/01/29/kQaiFJ.png)  

3. Mu顶部有个REPL按钮，REPL全称是(Read Eval Print Loop:交互式解释器)。常见的脚本语言例如js和python都有这样的一个快速编程执行的终端界面，后面我们简称`终端`

4. 找到Meowbit后我们就使用Mu连接上它的终端：在Mu顶端选择repl按钮，并在下方会出现喵比特的通信终端。

![](https://s2.ax1x.com/2019/01/29/kQalYd.png)

我们在终端输入如下代码并键盘按下回车，可以看到终端中主板也回应了一个Hello world回来。

```python
	print("hello world")
```

![](https://s2.ax1x.com/2019/01/29/kQa1fA.png)

!>因为喵比特的串口是软件模拟出来的，如果连接失败或在`终端`无法键入字符，则可能是连接断了，此时需要在此点击REPL按钮关闭终端并间断重复2次reset按键重新回到Micropython编程模式下，再点击REPL打开`终端`


## 初次交互

通常来说，与硬件的首次交互大都以点亮led的形式，好比软件入门的第一个helloworld程序。我们先在终端逐行敲下并回车如下代码  
```python
import time  
from pyb import LED  
led = LED(1)  
led.on()  
led.off()  
```

可以看到屏幕右上角的第一颗LED当输入完“led.on()”就亮了，当输入完“led.off()”就灭了

## 离线运行

REPL只是一个用于调试的交互环境，要真正掌控一款硬件最重要的就是自动化，那么将程序下载到硬件中便是这么一个目的。

在Mu的顶部工具栏选择加载喵比特上的main.py文件。

!>程序执行入口一定是main.py，并注意格式

![](https://s2.ax1x.com/2019/01/29/kQd9jP.png)

在编辑器界面修改代码为如下并保存

```python
import time   # 需要用到延时，所以导入time模块
from pyb import LED

led = LED(1)

while True:     # 需要开机后led持续亮灭循环
	led.on()
	time.sleep(1)  # 延时1s
	led.off()
	time.sleep(1)
```

!> 点了保存后，程序就会开始下载，下载期间右上角的绿灯会亮起，这个过程中一定不要按复位，等待绿灯熄灭即可

![](https://s2.ax1x.com/2019/01/29/kQdIUg.png)

由于喵比特只有在每次进入Micropython模式的时候才检测入口程序并执行，所以新下载的程序并不能被板子发现，我们需要间断按下2次复位(既回到bootloader主界面，再回到Micropython模式界面)此时就可以看到程序控制的LED灯一闪一闪了。

