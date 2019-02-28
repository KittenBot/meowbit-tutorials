# 按键检测  

喵bit上还有6个可编程的按键，如果使用过喵bit的makecode平台的同学可能会发现完全就是个可编程的游戏机。那么在micropython下是不是也能实现同样的功能呢？    

无奈小喵家人力资源有限，完整的micropython游戏引擎正在制作todo列表上逐步推进，这里就先用按键做一些简单的东西。

按键可以分为`直接读取按键值`和`按下事件`触发两种使用方式。

## 检测按键

喵bit的按键都是按下导通地，也就是当按下后按键对应的io读取值为0。打开mu后通过终端连上喵比特，这节内容比较简单我们直接在`终端`上写代码就行了。  

先试一下不按按键A时输入button.value()，再试试按下A回车执行，观察返回值     

```python
	from pyb import Pin
	button = Pin('BTNA', Pin.IN, Pin.PULL_UP)  
	# Pin(IO的名称, 读写方式，上拉/下拉)  
	button.value()
```  

!> Pin是IO配置函数，其中IO的名称6个按键分别对应UP,DOWN,LEFT,RIGHT,BTNA,BTNB

![](https://s2.ax1x.com/2019/01/29/kQy8Ln.png ':no-zoom')

## 按键中断

使用按键事件就是当按键按下后去执行某个函数，这时候我们需要micropython另外一个库ExtInt(外部中断库).

1.在中断逐行敲下下面代码  
```python
	from pyb import Pin, ExtInt
	
	def callback(line):
	    print("pressed =", line)

	extint = ExtInt('BTNA', ExtInt.IRQ_FALLING, Pin.PULL_UP, callback)
```  
  
2.试着按A键，可以看到中断返回的数字，既是当前按键的中断源  
  
<!-- ?>3.下面结合显示，将每个按键的中断源一口气测得。拷贝如下程序到main.py并保存  
   -->

其中中断回调函数callback的参数line是中断源，每个按键的中断源都不一样。