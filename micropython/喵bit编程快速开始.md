## 重要文件介绍  
    
?>成功刷了micropython模式后电脑会出现如下盘符，里面的文件详细意义如下:  

![](https://s2.ax1x.com/2019/01/29/kQYUPI.png)    

- boot.py 是启动文件，一上电micropython会最优先执行这个文件，一般包括所有运行环境和库文件的初始化。
- main.py 是用户的主程序，大家平时学习开发主要是编辑这个文件，喵bit准备就绪后会自动执行这个文件的代码。
- pybcdc.inf 是串口驱动程序，也是我们这一节需要的文件。
- README.txt 是micropython官方的说明文档

## 下载编程软件  
  
micropython模式下的编程软件我们推荐Mu editor - [下载地址](http://cdn.kittenbot.cn/mu/Mu_1.0.1.exe)

## 安装micropython的串口驱动
  
!>为了能让喵比特在Mu editor中通过REPL实现在线交互，我们需要像Microbit在kittenblock中那样有一个串口驱动。除了Win10和mac，可能其他系统需要通过手动方式安装串口驱动。

?>1.在设备管理器中可以看到这样一个没有驱动的硬件设备  

![](https://s2.ax1x.com/2019/01/29/kQNF74.png)  
  
?>2.右键点击这个设备，并选择更新驱动程序软件，之后选择下方的【浏览计算机以查找驱动程序软件】，并将搜索目录指向喵比特的盘符，下一步即可。  
  
![](https://s2.ax1x.com/2019/01/29/kQUBM6.png)  
  
?>3.驱动安装成功后大家可以看到电脑多出来一个新的串口设备  
  
![](https://s2.ax1x.com/2019/01/29/kQURJA.png)  
  
!>如果出现安装错误等安装失败的问题，请查阅  [解决串口驱动安装失败](meowbit驱动安装失败的问题解决)

## 通过Mu editor连接上喵比特


1. 首先我们打开Mu editor，之后将喵比特连接上电脑。  

2. 在Mu editor左上角的硬件框总选择meowbit，如果您安装了串口驱动也会发现Mu editor自动提示您找到喵bit并为您自动切换。

![](https://s2.ax1x.com/2019/01/29/kQaiFJ.png)

?>Mu顶部有个REPL按钮，REPL全称是(Read Eval Print Loop:交互式解释器)。常见的脚本语言例如js和python都有这样的一个快速编程执行的终端界面，后面我们简称`终端`

3. 找到Meowbit后我们就使用Mu连接上它的终端：在Mu顶端选择repl按钮，并在下方会出现喵比特的通信终端。

![](https://s2.ax1x.com/2019/01/29/kQalYd.png)

我们在终端输入如下代码并键盘按下回车，可以看到终端中主板也回应了一个Hello world回来。

```python
	print("hello world")
```

![](https://s2.ax1x.com/2019/01/29/kQa1fA.png)

!>因为喵比特的串口是软件模拟出来的，如果连接失败请照着Mu的提示复位喵bit并等待3s左右再重新连接。


## 与喵比特的第一次交互

通常来说，与硬件的首次交互大都以点亮led的形式，好比软件入门的第一个helloworld程序。我们先在终端一行行敲下并回车如下代码  

?>	import time  
	from pyb import LED  
	led = LED(1)  
	led.on()  
	led.off()  

可以看到屏幕右上角的第一颗LED当输入完“led.on()”就亮了，当输入完“led.off()”就灭了

## 尝试脱离电脑

REPL只是一个用于调试的交互环境，要真正掌控一款硬件最重要的就是自动化，那么将程序下载到硬件中便是这么一个目的。

在Mu的顶部工具栏选择加载喵比特上的main.py文件。

!>程序执行入口一定是main.py

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

?> 点了保存后，程序就会被下载进板子里，下载中右上角的绿灯会亮起，这个过程中一定不要按复位，需要等待右上角绿灯熄灭`

![](https://s2.ax1x.com/2019/01/29/kQdIUg.png)

!> 记住一定要保存，不然不生效。保存成功过后，需要按下侧面的复位键(这点是必须的)，就可以看到写的程序执行了，绿灯隔一秒亮灭一次

## REPL使用小窍门

- Micropython的REPL有自动补全功能， 若果你想知道pyb对象中到底有哪些方法和变量，那么你只需要敲如`pyb.`并按下Tab键，或者`pyb.L`按下Tab键，就可以补全为pyb.LED。平时在编程中推荐大家多用自动补全的功能，防止因为拼写错误。

- repl另外一个功能就是按键盘方向键↑可以快速调出之前执行过的命令，这样一些重复执行的命令就不需要再敲一遍了  

## 如何恢复通过REPL控制喵比特

当已经下载过程序，想要再回到REPL，只需要将u盘上的main.py里面的代码清空后保存

![](https://s2.ax1x.com/2019/01/29/kQdggI.png)

再复位主板就可以重新正常使用终端了~

`终端控制的好处就是所见即所得`，不用按复位按键什么的


?> 我们已经知道喵bit的u盘下有一个main.py文件，我们现在就要直接编辑这个文件，做出我们第一个程序。

!>如果你能看到喵比特的盘符，却有一些奇怪的问题，请参考 [FAQ](FAQ/FAQ)