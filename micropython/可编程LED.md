# 可编程led
  
![](https://s2.ax1x.com/2019/01/29/kQgdW8.png  ':no-zoom')

喵bit的右上角有两颗可编程的led，从左数分别绿灯LED(1),和红灯LED（2）。控制LED虽说作为硬件入门是最基本的一个项目，但其在任何一个大型项目的实际交互过程中的地位都是及其重要的（想想，LED不同颜色，不同的闪烁频率所代表的含义已经深入日常生活呢）

## 控制LED的方法
    
    on()      # 点亮
    off()     # 熄灭 
    toggle()  # 切换
	intensity([val])  #调节亮度实际是通过定时器的PWM来实现。没有参数情况下为获取LED亮度值。含有参数val时为设置led的亮度，val为0~255可调

除了on()和off()能够分别控制LED亮灭外，LED对象还提供了一个toggle()方法  
用处是在现有的状态上取反。也就是说若目前LED(1)状态为on()，则执行toggle()后，LED(1)显示为off()状态

---
## 例1：DISCO效果

使用方法toggle()来控制板载的两颗LED灯实现一个炫酷的disco效果

```python
from pyb import LED 
import time

leds = [LED(i) for i in range(1, 3)]   
# for i in range(1,3)意指i=1，i=2。如此leds = [LED(1),LED(2)]

# 由于toggle()需要知道现在的状态从而切换，所以在程序开始时需要将全部LED状态先置为off()
for l in leds: 
	l.off()
	
n = 0

while True:
    n = (n + 1) % 2  # 让n只能在0,1内取值
    leds[n].toggle()    
    time.sleep(0.05)  # 延时0.05s
```  

!>想知道自己写的程序是否有错误，推荐使用Mu提供检查功能


## 例2：呼吸灯

使用方法intensity()来控制led灯的

![](./image/led_02.png)  


```python
import pyb

led = pyb.LED(1)
led.off()

while True:
    for i in range (0, 256):  # 0-255
        led.intensity(i)
        pyb.delay(10)
    for i in range (255, -1, -1):  # 255-0
        led.intensity(i)
        pyb.delay(10)
```