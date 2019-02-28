在REPL中一行行敲下代码观察结果

```python
import time     #导入time模块

time.sleep(1)       #延时1秒
time.sleep_ms(500)  #延时500毫秒
time.sleep_us(10)   #延时10微妙

start = time.ticks_ms()     #获取当前毫秒计数器数值
time.sleep_ms(1000)         #
interval = time.ticks_diff(time.tick_ms(), start)   #计算时间差(现在时间， 开始时间)
```