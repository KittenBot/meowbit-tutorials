```python
from pyb import Pin    #引入引脚类
from pyb import ExtInt #引入中断类

btnA = Pin('BTNA', Pin.IN, Pin.PULL_UP) #以实例化按键A为例子
btnA.value()                            #读按键A的返回值

def callback(line):
	    print("up", line)      #定义回调函数

# 可用按键有："up","down","left","right","A","B"

ext = ExtInt(Pin('UP'),ExtInt.IRQ_FALLING, Pin.PULL_UP, callback)   #定义中断
 
```
