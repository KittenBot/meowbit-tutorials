```python
from pyb import Pin， Timer

p = Pin（'B8'）  #PB8所属 TIM4_CH3 
tim = Timer(4， freq = 1000)

ch = tim.channel(3， Timer.PWM， pin = p)  #（通道，模式， 引脚对象）
ch.pulse_width_percent(50)                #使用的初始脉宽值百分比
```