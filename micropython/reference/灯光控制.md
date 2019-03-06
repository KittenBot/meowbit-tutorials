```python
from pyb import LED

led = LED(1)  #两颗LED从左到右分别为LED（1），LED（2）

led.toggle()  #LED翻转
led.on()      #打开LED  
led.off()     #关闭LED
led.intensity([value])  #获取或设置led的亮度(0~255)
```