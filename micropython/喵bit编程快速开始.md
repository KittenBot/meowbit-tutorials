# 喵bit编程快速开始

在上一节我们已经知道喵bit的u盘下有一个main.py文件，我们现在就要直接编辑这个文件，做出我们第一个程序。

## mu-editor连接上喵bit

1. 首先我们打开mu-editor，之后将喵bit连接上电脑。
2. 在mu-editor左上角的硬件框总选择meowbit，如果您安装了串口驱动也会发现mu-editor自动提示您找到喵bit并为您自动切换。

![](./image/c3_01.png)

mu顶部有个repl按钮，repl全称是(Read Eval Print Loop:交互式解释器)。常见的脚本语言例如js和python都有这样的一个快速编程执行的终端界面，后面我们简称终端就好了~

找到喵bit后我们就使用mu连接上它的终端，在mu顶端选择repl按钮，并在下方会出现喵bit的通信终端。3. 找到喵bit后我们就使用mu连接上它的终端，在mu顶端选择repl按钮，并在下方会出现喵bit的通信终端。

![](./image/c3_02.png)

我们在终端输入如下代码并键盘按下回车，可以看到终端中主板也回应了一个Hello world回来。


	print("hello world")

![](./image/c3_03.png)

**注意：因为喵bit的串口是软件模拟出来的，如果连接失败请照着mu的提示复位喵bit并等待3s左右再重新连接。**


## 灯。。等灯等灯

硬件上的第一个helloworld程序，一般就是点灯程序。我们先在终端写下如下代码

	import time
	from pyb import LED
	led = LED(1)
	led.on()
	led.off()

可以看到lcd屏幕下方的LED当输入完“led.on()”就亮了，当输入完“led.off()”就灭了

## 写开机启动程序

现在我们写一个让喵bit开机就闪烁这个LED。。

在mu的顶部工具栏选择加载喵bit上的main.py文件。（注意是main.py）

![](./image/c3_04.png)

修改代码并保存。

	import time
	from pyb import LED
	led = LED(1)
	led.on()
	while True:
		time.sleep(1)
		led.toggle()

![](./image/c3_05.png)
## REPL使用小窍门

micropython的repl有自动补全功能，例如你可以敲`pyb.L`之后按下tab键就会弹出提示LED。也可以直接敲下`pyb.`之后按tab看看pyb对象中到底有哪些变量和方法。平时在编程中推荐大家多用自动补全的功能，防止因为拼写错误导致程序崩了那就很尴尬了~

repl另外一个功能就是按键盘方向键↑可以快速调出之前输过的命令，这样一些重复执行的命令就不需要再敲一遍了~
**注意：记住一定要保存，不然不生效**

## 测试程序是否能正确执行

按下主板顶部的复位按钮，可以看到屏幕下方的LED自动就开始闪烁了。

## 如何恢复通过终端控制喵bit？

只需要将u盘上的main.py里面的代码清空后保存

![](./image/c3_06.png)

再复位主板就可以重新连上去了~

终端控制的好处就是程序控制所见即所得，不用按复位按键什么的

