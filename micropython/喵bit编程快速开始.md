# 喵bit编程快速开始

在上一节我们已经知道喵bit的u盘下有一个main.py文件，我们现在就要直接编辑这个文件，做出我们第一个程序。

## mu-editor连接上喵bit

首先我们打开mu-editor，之后将喵bit连接上电脑。在mu-editor左上角的硬件框总选择meowbit，如果您安装了串口驱动也会发现mu-editor自动提示您找到喵bit并为您自动切换。

mu顶部有个repl按钮，repl全称是(Read Eval Print Loop:交互式解释器)。常见的脚本语言例如js和python都有这样的一个快速编程执行的终端界面，后面我们简称终端就好了~

找到喵bit后我们就使用mu连接上它的终端，在mu顶端选择repl按钮，并在下方会出现喵bit的通信终端。

我们在终端输入如下代码，可以看到终端中主板也回应了一个Hello world回来。


	print("hello world")


**注意：因为喵bit的串口是软件模拟出来的，如果连接失败请照着mu的提示复位喵bit并等待3s左右再重新连接。**


## 灯。。等灯等灯

硬件上的第一个helloworld程序，一般就是点灯程序。我们先在终端写下如下代码

	import time
	from pyb import LED
	led = LED(1)
	led.on()
	time.sleep(1)
	led.off()

可以看到lcd屏幕下方的led先亮了，之后隔了一秒又熄灭了

## 开机启动程序

还记得我们说过的main.py文件吗？现在我们让我们的喵bit开机就闪烁这个led。。

在mu的顶部工具栏选择打开喵bit上的main.py文件，将代码修改下并保存。

	import time
	from pyb import LED
	led = LED(1)
	led.on()
	while True:
		time.sleep(1)
		led.toggle()

## REPL使用小窍门

micropython的repl有自动补全功能，例如你可以敲`pyb.L`之后按下tab键就会弹出提示LED。也可以直接敲下`pyb.`之后按tab看看pyb对象中到底有哪些变量和方法。平时在编程中推荐大家多用自动补全的功能，防止因为拼写错误导致程序崩了那就很尴尬了~

repl另外一个功能就是按键盘方向键↑可以快速调出之前输过的命令，这样一些重复执行的命令就不需要再敲一遍了~

**注意：记住一定要保存，不然不生效**
	
这时候我们按下主板顶部的复位按钮，可以看到主板启动后led自动就开始闪烁了。细心的同学可能会发现这时候再也不能通过终端控制喵bit了，这是因为程序启动后一直有一个程序在运行，只有没有程序运行的时候终端才会交给用户控制。

那么怎么恢复呢？很简单只需要将u盘上的main.py里面的代码清空后保存，再复位主板就可以重新连上去了~

