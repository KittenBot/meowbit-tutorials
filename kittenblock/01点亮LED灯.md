# 点亮LED灯 

## 相关功能  

**积木块** 

![](https://s2.ax1x.com/2019/08/23/mDuTV1.png ':no-zoom')  

**对应Micropython方法**  

```python
led1.on()   # 控制LED灯1亮，灯2同理
led1.off()  # 控制LED灯1灭，灯2同理
led1.toggle()      #LED灯1状态切换
led1.intensity(x)  #x为LED灯1亮度值，灯2同理
```

##  LED入门项目——点亮LED灯  

**项目程序**

先快速体验LED的功能，搭建如下程序后点击箭头处的运行按钮

![](https://s2.ax1x.com/2019/08/23/mDuShT.png)  

**实验现象** 

LED灯亮1s，亮度变暗1s后灭掉 


## LED灯进阶项目——呼吸灯  

**项目程序**  
![](https://s2.ax1x.com/2019/08/23/mDl4W6.png ':no-zoom')  

我们不妨尝试用python在程序框中直接编写呼吸灯的程序（运行效果与上图程序是一样的）  
![](https://s2.ax1x.com/2019/08/23/mD1c1f.png ':no-zoom')  

图中代码如下：
```python
#/bin/python
from pyb import *
from time import sleep

led1 = LED(1)

while True:
  for i in range(50):
    led1.intensity(i)
    sleep(0.05)
  for i in range(50):
    led1.intensity(50 - i)
    sleep(0.05)
# 与积木块的程序相同，但是实现途径不一样，代码也简短不少
```

**实验现象** 
  
![](/images/m2_10.gif ':no-zoom')  
