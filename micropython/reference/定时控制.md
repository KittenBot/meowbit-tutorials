```python
from pyb import Timer 
from pyb import LED

tim = Timer(1, freq = 1000) #实例化一个timer对象，使用定时器4、设置频率为1000hz
tim.counter()   #查看计数值

tim = Timer(1)                           #实例化一个timer对象，使用定时器1
tim.init(freq = 1)                       #初始化设置触发频率为1HZ
tim.init(prescaler = 83, period = 999)   #初始化设置预分频器和定时器周期

tim.callback(lambda t: LED(1).toggle())  #通过回调方法，调用python函数
```

?>[定时器详解](micropython/detail/定时器详解)

